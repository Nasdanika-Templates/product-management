# Product Management Model Template

A starter template for authoring your own [Nasdanika product management model](https://product-management.models.nasdanika.org/). 
Create a repository from this repository as a template, enable GitHub pages with GitHub actions.
Edit YAML, push - a GitHub Action publishes the rendered documentation site to GitHub Pages for free.

**Example output:** https://nasdanika-templates.github.io/product-management/

## What this template gives you

When you instantiate this template you get:

- YAML files for personas, concerns, capabilities, and providers - the structure the metamodel expects
- A GitHub Actions workflow that builds your model into a documentation site
- Automatic publishing of that site to GitHub Pages on every push to `main`

## How to use it

1. **Use this template** to create your own repository (the green *Use this template* button at the top of the GitHub UI).
2. **Enable GitHub Pages** in your new repository's *Settings ? Pages*, with the source set to *"GitHub Actions"*.
3. **Edit the YAML files** to describe your own personas, concerns, capabilities, and providers. The examples in the template are illustrative - replace them with your own.
4. **Push to `main`.** The workflow runs, builds the site, publishes to `https://<your-org>.github.io/<your-repo>/`.

## How the build works

The GitHub Actions workflow invokes the Nasdanika CLI's [`model/html-app/site`](https://docs.nasdanika.org/nsd-cli/nsd/model/html-app/site/index.html) command pipeline.
The pipeline:

1. Loads your YAML model files
2. Resolves references 
3. Renders the resulting graph as an interactive documentation site
4. Publishes the result to the GitHub Pages

The CLI is open source. The pipeline is deterministic. The site is the output; the model is the source.

## Authoring Markdown content

Descriptions in the model accept Markdown as the default authoring format.
For richer documentation embedded directly in version-controlled text, see the [drawio-site template](https://nasdanika-templates.github.io/drawio-site/) - its conventions for Markdown authoring with draw.io diagrams embedded inline apply here as well.

## Next steps

- Read the [full documentation](https://product-management.models.nasdanika.org/) for the metamodel
- Browse the [example site](https://nasdanika-templates.github.io/product-management/) generated from this template

## License

EPL-2.0 (template). Your derived model's license is your choice.
