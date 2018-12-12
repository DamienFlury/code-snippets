# C

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
