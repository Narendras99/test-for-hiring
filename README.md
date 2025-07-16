using System;
using System.IO;

public enum FileOperation
{
    Copy,
    Move,
    Delete
}

public record FileCommand(string SourcePath, string DestinationPath, FileOperation Operation)
{
    public void Execute()
    {
        try
        {
            switch (Operation)
            {
                case FileOperation.Copy:
                    File.Copy(SourcePath, DestinationPath, overwrite: true);
                    break;

                case FileOperation.Move:
                    File.Move(SourcePath, DestinationPath);
                    break;

                case FileOperation.Delete:
                    File.Delete(SourcePath);
                    break;

                default:
                    throw new InvalidOperationException("Invalid operation.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error during file operation: {ex.Message}");
            throw;
        }
    }
}
