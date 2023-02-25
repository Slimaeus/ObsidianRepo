# 1️⃣Packages
---
| | Name | Version |
|-|-|-|
|1| Unity | 5.11.10
|2| Unity.WebAPI | 5.4.0

# 2️⃣Steps
---
## 1. Add code to Global.asax.cs
```csharp
protected void Application_Start()
{
	var container = new UnityContainer(); //Init-Dependency-Injection-Container

	container.RegisterType<YourDbContext>(new InjectionConstructor());
	
	container.RegisterFactory<UserStore<AppUser>>(
		c => new UserStore<AppUser>(c.Resolve<DataContext>())    
	);
	container.RegisterFactory<UserManager<AppUser>>(
		c => new UserManager<AppUser>(c.Resolve<UserStore<AppUser>>())
	);

	//Config-AutoMapper
	var config = new MapperConfiguration(cfg =>
	{
		cfg.AddProfile(new MappingProfile());
	});
	container.RegisterInstance(config.CreateMapper());

	AreaRegistration.RegisterAllAreas();
	GlobalConfiguration.Configure(WebApiConfig.Register);

	GlobalConfiguration.Configuration.DependencyResolver = new UnityDependencyResolver(container); //Config-Dependency-Injection

	FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
	RouteConfig.RegisterRoutes(RouteTable.Routes);
	BundleConfig.RegisterBundles(BundleTable.Bundles);
}
```
## 2. Use get the instance of injected types

```csharp
public class YourController : ApiController
{
	private readonly DataContext db;
	private readonly IMapper mapper;

	public YourController(DataContext context, IMapper mapper)
	{
		db = context;
		this.mapper = mapper;
	}
}
```

# 3️⃣Links

- [Dependency injection - Wikipedia](https://en.wikipedia.org/wiki/Dependency_injection#:~:text=In%20software%20engineering%2C%20dependency%20injection,leading%20to%20loosely%20coupled%20programs.)
