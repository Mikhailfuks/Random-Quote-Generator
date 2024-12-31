using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

public class RandomQuoteGenerator
{
    // Option 1: Quotes in a List
    private static List<string> quotes = new List<string>
    {
        "The only way to do great work is to love what you do. - Steve Jobs",
        "Strive not to be a success, but rather to be of value. - Albert Einstein",
        "Life is what happens when you're busy making other plans. - John Lennon",
        "The best way to predict the future is to create it. - Peter Drucker",
        "Be the change that you wish to see in the world. - Mahatma Gandhi"
    };

    // Option 2: Quotes from a Text File (quotes.txt)
    private static List<string> LoadQuotesFromFile(string filePath)
    {
       List<string> fileQuotes = new List<string>();
        try
        {
            fileQuotes = File.ReadAllLines(filePath).Where(line => !string.IsNullOrWhiteSpace(line)).ToList();
        }
        catch (Exception ex)
        {
             Console.WriteLine($"Error reading quotes from file: {ex.Message}");
            return new List<string>();
        }
       return fileQuotes;
    }

    public static string GetRandomQuote()
    {
        List<string> allQuotes = quotes;
        //Uncomment this line if you want to load from file instead of the hardcoded list
        //allQuotes = LoadQuotesFromFile("quotes.txt");


        if (allQuotes.Count == 0)
        {
            return "No quotes available.";
        }

        Random random = new Random();
        int randomIndex = random.Next(allQuotes.Count);
        return allQuotes[randomIndex];
    }

    public static void Main(string[] args)
    {
        Console.WriteLine("Random Quote:");
        Console.WriteLine(GetRandomQuote());
        Console.ReadKey(); // Keep console open until key is pressed
    }
}
