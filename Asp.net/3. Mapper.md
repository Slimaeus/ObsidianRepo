# 1️⃣Packages
---
| | Name | Version |
|-|-|-|
|1| AutoMapper | 8.1.1|

# 2️⃣Steps
---
## 1. Create Mapping Profile

```csharp
public class MappingProfile : Profile
    {
        public MappingProfile()
        {
            CreateMap<Entity, EntityDTO>();
            CreateMap<CreateEntityDTO, Entity>();
            CreateMap<EditEntityDTO, Entity>()
                .ForAllMembers(options =>
                {
                    options.Condition((src, des, srcValue, desValue) => srcValue != null);
                });
        }
    }
```

## 2. Add Mapping Profile to config

```csharp
var config = new MapperConfiguration(cfg =>
            {
                cfg.AddProfile(new MappingProfile());
            });
```

## 3. Add to container (Dependency Injection)

```csharp
container.RegisterInstance(config.CreateMapper());
```

## 4. Use it in Controller example 

```csharp
public class ProjectsController : ApiController
{
	private readonly DataContext db;
	private readonly IMapper mapper;

	public ProjectsController(DataContext context, IMapper mapper) 
	{
		db = context;
		mapper = mapper;
	}
	public async Task<IHttpActionResult> GetEntity(Guid id)
	{
		Entity entity = await db.Entities.FindAsync(id);
		EntityDTO entityDTO = mapper.Map<EntityDTO>(entity);
		if (entity == null)
		{
			return NotFound();
		}
		return Ok(entityDTO);
	}
}
```
