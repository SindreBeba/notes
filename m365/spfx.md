# SharePoint Framework (SPFx)

> **Source:**
>
> [Sections "Overview", "Why the SharePoint Framework", "Getting started", and "Web parts" - SharePoint Framework (Microsoft Docs)](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview)

## Interesting sections

- [Key features of the SharePoint Framework](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview#key-features-of-the-sharepoint-framework)

## Basic web part and property pane

Any client-side web part should extend the `BaseClientSideWebPart` class to be defined as a valid web part. Below is a simplified example of a `HelloWorld` web part.

```tsx
export interface IHelloWorldWebPartProps { // Interface for the property pane
	description: string;
}

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {

  protected onInit(): Promise<void> {
    return super.onInit();
  }
  
  public render(): void {
    this.domElement.innerHTML = "<div>Render of your site</div>";
  }
  
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [{
        header: { description: strings.PropertyPaneDescription },
        groups: [{
          groupName: strings.BasicGroupName,
          groupFields: [
            PropertyPaneTextField('description', { label: strings.DescriptionFieldLabel })
          ]
        }]
      }]
    };
  }
}
```

The property pane is where you can define properties to customize your web part. The default values for the property pane are defined in the `HelloWorldWebPart.manifest.json` file.

```json
"preconfiguredEntries": [{
  "properties": {
    "description": "HelloWorld"
  }
}]
```

## Developer tools

**Yeoman** can be used to scaffold a project.

**Gulp** is the bundler used for SPFx projects. It's used by Microsoft in their examples, but I'm not sure if it's required.

```sh
gulp trust-dev-cert
gulp serve # runs the webpart locally and can be opened in SharePoint workbench
```

### Side Loading

You can side load an SPFx application to make it easier to develop and see the changes you make in a live installation.

1. Package the application for production.
2. Upload it to the app catalog and install it on a site.
3. Create a modern page and add the web part to it.
4. Add the parameter `?debug=true&noredir=true&debugManifestsFile=http://localhost:4321/temp/manifests.js` to the URL.

## Other features

**manifest.json** - The manifest file is also where you define the version, ID, display name, icon, and description of the web part.
