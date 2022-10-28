```xaml
<TextBlock>
    <TextBlock.Text>    
        <MultiBinding StringFormat="{}{0} + {1}">
            <Binding Path="Name" />
            <Binding Path="ID" />
        </MultiBinding>
    </TextBlock.Text>
</TextBlock>
```

