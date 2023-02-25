# 1️⃣ Packages:

- Microsoft.AspNet.Identity.EntityFramework
- Swashbukle

# 2️⃣ Steps
1. Add AppUser model and IdentityDbContext
2. Config connection string
3. Migrate to database
	1. Enable-Migrations (Update Entity Framework if error appear)
	2. Add-Migration {Migration Name}
	3. Update-Database
4. Generate Controller or Create Controller
	1. Right click on Controllers folder -> Add -> Click Controller
	2. Choose Web API in the right side bar
	3.  1. Generate:
		1. Choose Web API 2 Controller with actions, using Entity Framework
		2. Click Add or Enter
		3. Choose the Entity class that you want to create a controller.
		4. Choose the Database context
		5. Change the controller name if you want
		6. Click Ok
	4. 2. Create
		1. Choose Web API 2 Controller - Empty