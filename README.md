# -Book-API
A simple ASP.NET Core Web API to manage books. Provides a single endpoint to get a list of books.

Features

    ASP.NET Core: Utilizes ASP.NET Core for a robust and scalable web API.
    Books Endpoint: Single endpoint to retrieve a list of books.
    MVC Design Pattern: Ensures clean code separation.

Endpoints

    GET /api/books: Returns a list of books with their ID, title, and author.

Models
Book

csharp

namespace BookApi.Models
{
    public class Book
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Author { get; set; }
    }
}

Controllers
BooksController

csharp

using Microsoft.AspNetCore.Mvc;
using BookApi.Models;

namespace BookApi.Controllers
{
    [Route("api/[Controller]")]
    [ApiController]
    public class BooksController : ControllerBase
    {
        private Book[] _books = new Book[]
        {
            new Book { Id = 1, Author = "Author One", Title = "Book One" },
            new Book { Id = 2, Author = "Author Two", Title = "Book Two" },
            new Book { Id = 3, Author = "Author Three", Title = "Book Three" },
        };

        [HttpGet]
        public ActionResult<IEnumerable<Book>> GetBooks()
        {
            return Ok(_books);
        }
    }
}

Program
Program.cs

csharp

namespace BookApi
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var builder = WebApplication.CreateBuilder(args);

            // Add services
            builder.Services.AddControllers();

            var app = builder.Build();

            // Add mapping
            app.MapControllers();

            app.MapGet("/", () =>
            {
                return Results.Redirect("/api/books");
            });

            app.Run();
        }
    }
}

Getting Started

    Clone the repository:

    bash

git clone https://github.com/your-username/BookApi.git

Navigate to the project directory:

bash

cd BookApi

Build and run the project:

bash

dotnet run

Access the API at https://localhost:7009/api/books.
