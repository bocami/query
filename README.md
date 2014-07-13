query
=====

```csharp
public class IsUserNameAvailableQuery : IQuery
{
  public string UserName { get; set;}
}

```

```csharp
public class IsUserNameAvailableQueryResult : IQueryResult
{
  public bool IsUserNameAvailable { get; set;}
}

```

```csharp
public class IsUserNameAvailableQueryHandler : IQueryHandler<IsUserNameAvailableQuery, IsUserNameAvailableQueryResult>
{
  private readonly IUserNameRepository userNameRepository;
  
  public IsUserNameAvailableQueryHandler(IUserNameRepository userNameRepository)
  {
    if(userNameRepository == null)
      throw new ArgumentNullException("userNameRepository");
      
    this.userNameRepository = userNameRepository;
  }
  
  public IsUserNameAvailableQueryResult Handle(IsUserNameAvailableQuery query) 
  {
    var isUserNameAvailable = userNameRepository.All(userName => userName != query.UserName);
    
    return new IsUserNameAvailableQueryResult
    {
      IsUserNameAvailable = isUserNameAvailable
    };
  }
}

```
