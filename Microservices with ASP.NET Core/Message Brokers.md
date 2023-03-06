# 1️⃣RabbitMQ
---
## 📦Packages
---
|Name|Version|
|-|-|
|RabbitMQ.Client|Newest|
## 🚶‍♂️Steps
---
### 🌟Producer
- IRabbitMQProducer interface
```csharp
public interface IRabbitMQProducer
    {
        void SendMessage<T>(T message);
    }
```
- RabbitMQProducer class
```csharp
public class RabbitMQProducer : IRabbitMQProducer
{
	private readonly ConnectionFactory _factory;

	public RabbitMQProducer(IOptions<RabbitMQConfiguration> options)
	{
		var rabbitMQConfiguration = options.Value;
		_factory = new ConnectionFactory
		{
			VirtualHost = rabbitMQConfiguration.VirtualHost,
			HostName = rabbitMQConfiguration.HostName,
			UserName = rabbitMQConfiguration.UserName,
			Password = rabbitMQConfiguration.Password,
			Port = rabbitMQConfiguration.Port
		};
	}
	public void SendMessage<T>(T message)
	{
		using var connection = _factory.CreateConnection();
		using var channel = connection.CreateModel();

		var queueName = "Your queue name";

		channel.QueueDeclare(queueName, exclusive: false);

		var json = JsonConvert.SerializeObject(message);
		var body = Encoding.UTF8.GetBytes(json);

		channel.BasicPublish(exchange: "", routingKey: queueName, body: body);
	}
}
```
### 📨Consumer
- Console's Program.cs file
```csharp
using Newtonsoft.Json;
using RabbitMQ.Client;
using RabbitMQ.Client.Events;
using System.Text;

var factory = new ConnectionFactory
{
    VirtualHost = "Virtual host",
    HostName = "Host name",
    UserName = "User name",
    Password = "Password",
    Port = 5672
};

using var connection = factory.CreateConnection();
using var channel = connection.CreateModel();

var queueName = "Your queue name";

channel.QueueDeclare(queueName, exclusive: false);

var consumer = new EventingBasicConsumer(channel);

Console.WriteLine("Ready...");

consumer.Received += (model, eventArgs) => {
    Console.WriteLine("Received");
    var body = eventArgs.Body.ToArray();
    var json = Encoding.UTF8.GetString(body);
    var message = JsonConvert.DeserializeObject<Message>(json);
    Console.WriteLine($"{message.Author}'s message received: {message.Content}");
};

channel.BasicConsume(queueName, autoAck: true, consumer: consumer);

Console.ReadKey();

public class Message
{
    public int Id { get; set; }
    public string Content { get; set; }
    public string Title { get; set; }
    public string Author { get; set; }
}
```

# 2️⃣Kafka
---
