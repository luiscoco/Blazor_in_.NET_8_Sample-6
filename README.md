# Blazor in .NET 8: Sample 6

Let's move toward a scenario where you can create reusable and customizable Blazor components, focusing on component composition and templating.

Example: Card Component

Features Demonstrated:

Component Composition: Building more complex components by nesting simpler ones.

Templating: Providing flexible layouts and content injection within components.

Parameter Customization: Making components adaptable to different data and styles.

Setup

Project: Create a new Blazor Server project (or use an existing one). You might name it "ComponentShowcase".

Components

Card.razor: (Inside the Shared folder – it’s a common practice)

```cshtml
<div class="card" @attributes="AdditionalAttributes">
    @if (Header != null)
    {
        <div class="card-header">
            @Header 
        </div>
    }
    <div class="card-body">
        @ChildContent
    </div>
    @if (Footer != null) 
    {
        <div class="card-footer">
            @Footer 
        </div>
    }
</div>

@code {
    [Parameter] public RenderFragment Header { get; set; }
    [Parameter] public RenderFragment ChildContent { get; set; }
    [Parameter] public RenderFragment Footer { get; set; }
    [Parameter(CaptureUnmatchedValues = true)] public Dictionary<string, object> AdditionalAttributes { get; set; }
}
```

Using the Card Component (e.g., in Index.razor):

```cshtml
@page "/"

<Card>
    <Header>
        <h3>Product Card</h3>
    </Header>
    <ChildContent>
        <p>A fantastic product description goes here.</p>
        <img src="product_image.jpg" alt="Product Image" class="img-fluid">
    </ChildContent>
    <Footer>
        <button class="btn btn-primary">Buy Now</button>
    </Footer>
</Card>
```

Explanation

RenderFragment: A powerful type that allows you to pass markup and components as content.

ChildContent: The core content area of the card.

Header and Footer: Optional sections for customized card layouts.

AdditionalAttributes: Captures any extra attributes (e.g., CSS classes or styles) to apply to the root card element.

Points to Note

Blazor's templating with RenderFragment gives you immense flexibility in how components are structured.

You can create multiple variations of the Card component (e.g., ImageCard, AlertCard) by providing different header, footer, and content combinations.

