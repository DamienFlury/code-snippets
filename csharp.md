# C#

## Connect to active directory

### Install `Microsoft.Windows.Compatibility`

```console
dotnet add package Microsoft.Windows.Compatibility
```

### Example

```csharp
const string ldapDomain = "x.x.x:###";

using (var context =
    new PrincipalContext (ContextType.Domain, ldapDomain))
using (var searcher = new PrincipalSearcher (new UserPrincipal (context))) {
    foreach (var person in searcher.FindAll ().Select (result => result.GetUnderlyingObject () as DirectoryEntry)) {
        Console.WriteLine ("First Name: " + person.Properties["givenName"].Value);
        Console.WriteLine ("Last Name : " + person.Properties["sn"].Value);
        Console.WriteLine ("SAM account name   : " + person.Properties["samAccountName"].Value);
        Console.WriteLine ("User principal name: " + person.Properties["userPrincipalName"].Value);
        Console.WriteLine ();
    }
}
```

## Add Swagger to API project

### Install `NSwag.AspNetCore`

```console
dotnet add package NSwag.AspNetCore
```

### ConfigureServices

```csharp
services.AddSwaggerDocument (options =>
{
    options.Title = "EmployeeAPI";
    options.OperationProcessors.Add (
        new OperationSecurityScopeProcessor ("JWT token")
    );
});
```

### Configure

```csharp
if (env.IsDevelopment ())
{
    app.UseSwagger ();
    app.UseSwaggerUi3 ();
}
```
