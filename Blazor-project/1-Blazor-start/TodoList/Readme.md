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

<h3>Todo</h3>

<ul>
    @foreach (var todo in todos)
    {
        <li>@todo.Title</li>
    }
</ul>

@code {
    private List<TodoItem> todos = new();
}

```
