Source:

https://learn.microsoft.com/en-us/aspnet/core/blazor/tutorials/build-a-blazor-app?view=aspnetcore-8.0


Steps:


1. dotnet new blazor -o TodoList

2. cd TodoList

3. dotnet new razorcomponent -n Todo -o Components/Pages

4. edit `Todo.razor` file

``` razor
@page "/todo"
@rendermode InteractiveServer

<PageTitle>Todo</PageTitle>

<h3>Todo</h3>

@code {

} 

```

5. add the `Todo` component to the navigation bar.

in the `Components/Layout/NavMenu.razor`

``` razor
<div class="nav-item px-3">
    <NavLink class="nav-link" href="todo">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
    </NavLink>
</div>

```

6. Add a `TodoItem.cs` file to the root of the project.

`TodoItems.cs`

``` cs
public class TodoItem
{
    public string? Title { get; set; }
    public bool IsDone { get; set; }
}
```

7. Edit code in `Components/Pages/Todo.razor`

``` razor
@page "/todo"
@rendermode InteractiveServer

<PageTitle>Todo</PageTitle>

<h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>

<ul>
    @foreach (var todo in todos)
    {
        <li>
            <input type="checkbox" @bind="todo.IsDone" />
            <input @bind="todo.Title" />
        </li>
    }
</ul>

<input placeholder="Something todo" @bind="newTodo" />
<button @onclick="AddTodo">Add todo</button>
 
@code {
    private List<TodoItem> todos = new();
    private string? newTodo;

    private void AddTodo()
    {
        if (!string.IsNullOrWhiteSpace(newTodo))
        {
            todos.Add(new TodoItem { Title = newTodo });
            newTodo = string.Empty;
        }
    }
}

```
