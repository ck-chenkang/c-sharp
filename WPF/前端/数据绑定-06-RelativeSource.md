[How do i use wpf binding with RelativeSource](https://stackoverflow.com/questions/84278/how-do-i-use-wpf-bindings-with-relativesource)

1. If you want to bind to another property on the object:

```xml
{Binding Path=PathToProperty, RelativeSource={RelativeSource Self}}
```

2. If you want to get a property on an ancestor:

```xml
{Binding Path=PathToProperty,
    RelativeSource={RelativeSource AncestorType={x:Type typeOfAncestor}}}
```

3. If you want to get a property on the templated parent (so you can do 2 way bindings in a ControlTemplate)

```xml
{Binding Path=PathToProperty, RelativeSource={RelativeSource TemplatedParent}}
```

or, shorter (this only works for OneWay bindings):

```xml
{TemplateBinding Path=PathToProperty}
```

