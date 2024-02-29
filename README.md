# Chinook Snippets

VisualStudio Extension providing code snippets for Chinook libraries.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

## Getting Started

1. Install the `Chinook Snippets` Visual Studio Extension
    * Download the `.vsix` directly from the [Visual Studio Marketplace - Chinook Snippets](https://marketplace.visualstudio.com/items?itemName=nventivecorp.ChinookSnippets).
    * Install it directly in Visual Studio <br/> ![image](/doc/images/vsstudioinstall.png)

2. Start writing `ck` and a list of snippets will appear. Choose any of the available Chinook snippets and press the `TAB` key to execute the snippet.
<br/> ![image](/doc/images/firstsnippet.gif) ![image](/doc/images/firstsnippet2.gif)

## Features

Explore the powerful features of the Chinook Snippets Visual Studio Extension. Easily enhance your projects with dynamic properties, commands, and DataLoader support using these convenient code snippets.

### DynamicProperty
On projects that uses [Chinook.DynamicMvvm](https://github.com/nventive/Chinook.DynamicMvvm), there are a couple of snippets available for creating dynamic properties. Writing `ckprop` will display all the available snippets. ![image](/doc/images/ckprop.png)

#### From Observable

- Write and execute `ckpropo` to create a two-way DynamicProperty from an observable.
```cs
public int MyProperty
{
	get => this.GetFromObservable<int>(ObserveMyProperty(), initialValue: 0);
	set => this.Set(value);
}

private IObservable<int> ObserveMyProperty()
{
	throw new NotImplementedException();
}
```
- Write and execute `ckpropog` to create a one-way DynamicProperty from an observable.
```cs
public int MyProperty => this.GetFromObservable<int>(ObserveMyProperty(), initialValue: 0);

private IObservable<int> ObserveMyProperty()
{
	throw new NotImplementedException();
}
```

#### From Task

- Write and execute `ckpropt` to create a two-way DynamicProperty from a `Task`.
```cs
public int MyProperty
{
	get => this.GetFromTask<int>(GetMyProperty, initialValue: 0);
	set => this.Set(value);
}

private async Task<int> GetMyProperty(CancellationToken ct)
{
	throw new NotImplementedException();
}
```
- Write and execute `ckproptg` to create a one-way DynamicProperty from a `Task`.
```cs
public int MyProperty => this.GetFromTask<int>(GetMyProperty, initialValue: 0);

private async Task<int> GetMyProperty(CancellationToken ct)
{
	throw new NotImplementedException();
}
```

#### From Value

- Write and execute `ckpropv` to create a two-way DynamicProperty from a value.
```cs
public int MyProperty
{
	get => this.Get<int>(initialValue: 0);
	set => this.Set(value);
}
```
- Write and execute `ckpropvg` to create a one-way DynamicProperty from a value.
```cs
public int MyProperty => this.Get<int>(initialValue: 0);
```

### DynamicCommand
On projects that uses [Chinook.DynamicMvvm](https://github.com/nventive/Chinook.DynamicMvvm), there are a couple of snippets available for creating commands. Writing `ckcmd` will display all the available snippets. ![image](/doc/images/ckcmd.png)


#### From Action
- Write and execute `ckcmda` to create a `IDynamicCommand` from an `Action`.
```cs
public IDynamicCommand MyCommand => this.GetCommand(() =>
	{

	});
```
- Write and execute `ckcmdap` to create a `IDynamicCommand` from an `Action`. with a parameter.
```cs
public IDynamicCommand MyCommand => this.GetCommand<int>(parameter =>
	{

	});
```

#### From Task
- Write and execute `ckcmdt` to create a `IDynamicCommand` from a `Task`.
```cs
public IDynamicCommand MyCommand => this.GetCommandFromTask(async ct =>
	{

	});
```
- Write and execute `ckcmdtp` to create a `IDynamicCommand` from a `Task`. with a parameter.
```cs
public IDynamicCommand MyCommand => this.GetCommandFromTask<int>(async (ct, parameter) =>
	{

	});
```

### DataLoader
On projects that uses [Chinook.DataLoader](https://github.com/nventive/Chinook.DataLoader), you can use the following snippet to create dataloaders:

- Write and execute `ckdl` to create a `IDataLoader`.
```cs
public IDataLoader<int> MyDataLoader => this.GetDataLoader(LoadMyDataLoader);

private async Task<int> LoadMyDataLoader(CancellationToken ct, IDataLoaderRequest request)
{
	return default(int);
}
```
- Write and execute `ckdlv` to create a `DataLoaderViewState` for x:Bind (Chinook.DataLoader.WinUI only)
```cs
public class DataLoaderViewState_int : DataLoaderViewState
{
	public DataLoaderViewState_int(DataLoaderViewState dataLoaderViewState) : base(dataLoaderViewState)
	{
		Data = (int)dataLoaderViewState.Data;
	}

	public new int Data { get; }
}

public class DataLoaderView_int : DataLoaderView
{
	public DataLoaderView_int()
	{
		Style = App.Current.Resources[typeof(DataLoaderView)] as Style;
	}

	protected override void SetState(DataLoaderViewState state)
	{
		var typedState = new DataLoaderViewState_int(state);
		base.SetState(typedState);
	}
}
```
- Write and execute `ckdlvx` to add a `DataLoaderView` (Chinook.DataLoader.WinUI only)
```xaml
<local:DataLoaderView_int Source = "{x:Bind DataLoader}" >
  <DataTemplate x:DataType="local:DataLoaderViewState_int">
  </DataTemplate>
</local:DataLoaderView_int>
```

## Breaking changes

Please consult [BREAKING_CHANGES.md](BREAKING_CHANGES.md) for more information about version
history and compatibility.

## License

This project is licensed under the Apache 2.0 license - see the
[LICENSE](LICENSE) file for details.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on the process for
contributing to this project.

Be mindful of our [Code of Conduct](CODE_OF_CONDUCT.md).

Make sure you read [this guide](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-distribute-code-snippets) on how to distribute code snippets.