# 037 Caching

## Lecture

[![# Caching](https://img.youtube.com/vi/PuPd9aZ55O4/0.jpg)](https://www.youtube.com/watch?v=PuPd9aZ55O4)

## Instructions

- In `HomeEnergyApi/Program.cs`
  - Add the line `builder.Services.AddMemoryCache()` right before `builder.Build()` is called

- In `HomeEnergyApi/Services/ZipCodeLocationService.cs`
  - On `ZipCodeLocationService`
    - Add a private readonly property of type `IMemoryCache`
    - Add a private readonly property of type `ILogger<ZipCodeLocationService>`
    - Add a private const property of type `string` named `CacheKey` with the value `"CachedZipCodeLocation"`
    - Add the newly created properties of types `IMemoryCache` and `ILogger<ZipLocationService>` to the argument list and assign them in the constructor
    - Modify the `Report()` method
      - IF the result of calling `TryGetValue()` with the `string CacheKey` provided as an argument and an out value of type `Place` designated on the `IMemoryCache` returns true
        - Call `LogInformation` on the `ILogger<ZipLocationService>` and supply the argument `$"Returning place from cache for {zipCode}"`
        - Return the out value of type `Place`
      - Otherwise, call `LogInformation` on the `ILogger<ZipLocationService>` and supply the argument `$"Fetching place from api for {zipCode}"`
      - Before returning the variable `Place place` call `Set()` on the `IMemoryCache` with the arguments `CacheKey`, the `Place place` variable, and `TimeSpan.FromSeconds(15)`

## Additional Information

- Do not remove or modify anything in `HomeEnergyApi.Tests`
- Some Models may have changed for this lesson from the last, as always all code in the lesson repository is available to view
- Along with `using` statements being added, any packages needed for the assignment have been pre-installed for you, however in the future you may need to add these yourself

## Building toward CSTA Standards:

- Document design decisions using text, graphics, presentations, and/or demonstrations in the development of complex programs (3A-AP-23) https://www.csteachers.org/page/standards
- Systematically design and develop programs for broad audiences by incorporating feedback from users (3A-AP-19) https://www.csteachers.org/page/standards

## Resources

- https://swagger.io/
- https://github.com/dotnet/aspnet-api-versioning/wiki/API-Documentation

Copyright &copy; 2025 Knight Moves. All Rights Reserved.
