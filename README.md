# 037 Caching

## Lecture

[![# Caching](https://img.youtube.com/vi/PuPd9aZ55O4/0.jpg)](https://www.youtube.com/watch?v=PuPd9aZ55O4)

## Instructions

- In `HomeEnergyApi/Security/ValueEncryptor.cs`
    - On ValueEncryptor create a new public delegate with void return type named `DecryptionHandler` taking two arguments of type `string` corresponding to the cipher text and plain text
    - On ValueEncryptor Create a new public event with type `DecryptionHandler?` named `ValueDecrypted`
    - Modify the `Decrypt()` method so that `Invoke()` is called on `ValueDecrypted` with the `cipherText` and `plaintext` passed as arguments, this should happen right before the `plaintext` is returned

- In `HomeEnergyApi/Services/DecryptionAuditService`
- Create a new public class `DecryptionAuditService`
  - Create a private readonly `ILogger<DecryptionAuditService>` property
  - Create a constructor that accepts an `ILogger<DecryptionAuditService>`
    - Assign the passed argument to the `ILogger<DecryptionAuditService>` property
  - Create an `OnValueDecrypted()` method that returns void and takes two arguments of type `string` corresponding to the cipher text and plain text 
    - Call the `LogInformation()` method on the `ILogger<DecryptionAuditService>` and pass the argument `$"[Audit] Decrypted: {cipherText} to {plaintext}"`

- In `HomeEnergyApi/Services/DecryptionLoggingService`
- Create a new public class `DecryptionLoggingService`
  - Create a private readonly `ILogger<DecryptionLoggingService>` property
  - Create a constructor that accepts an `ILogger<DecryptionLoggingService>`
    - Assign the passed argument to the `ILogger<DecryptionLoggingService>` property
  - Create an `OnValueDecrypted()` method that returns void and takes two arguments of type `string` corresponding to the cipher text and plain text 
    - Call the `LogInformation()` method on the `ILogger<DecryptionAuditService>` and pass the argument `$"[Logging] Decrypted: {cipherText} to {plaintext}`

- In `HomeEnergyApi/Program.cs`
- Add two singletons for `DecryptionAuditService` and `DecryptionLoggingService` to the `Services` property on the builder
- Within the scope of `app.Services.CreateScope()`...
    - Utilize `scope.ServiceProvider.GetRequiredService()` to get the `ValueEncryptor`, `DecryptionAuditService`, and `DecryptionLoggingService`
    - Assign the delegate services `DecryptionAuditService` and `DecryptionLoggingService` to the `ValueDecrypted` event on the `ValueEncryptor`

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
