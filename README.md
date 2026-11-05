# Felt Platform Inventory

Interactive dashboard mapping all codebases, tools, and infrastructure owned by the Felt Platform team.

## Live site

Hosted on GitHub Pages — just push to `main` and the dashboard is live.

## Local development

```bash
cd felt-platform-inventory
npx serve
```

Then open [http://localhost:3000](http://localhost:3000)

Any static file server works — `python -m http.server`, `php -S localhost:8000`, etc. The HTML fetches the YAML at runtime, so both files must be served from the same directory.

Opening the HTML directly as a `file://` URL won't work (browsers block `fetch` from the file protocol).

## Updating the inventory

Edit `felt-platform-inventory.yaml`.

### Adding an item

Add an entry under the appropriate area's `items` list:

```yaml
- name: my-new-repo
  npm-name: @rh-felt/my-new-repo
  url: https://github.com/patternfly/my-new-repo
  npm-url: https://npmjs.org/packages/@rh-felt/my-new-repo
  platform: GitHub
  org: patternfly
  status: active
  description: What this repo does
  contacts: [Person Name]
  dependsOn: [patternfly-react]    # optional — shows arrows in the graph
  consumers: [some-other-repo]     # optional — reverse dependency arrows
  tags: [dependency, personal]     # optional — shown as labels on the card
  notes: Any additional context.   # optional
```

Only `name`, `status`, and `description` are required. All other fields default to empty. `npm-name` and `npm-url` are not currently displayed in the UI.

### Adding a new area

Add a new entry to the top-level `areas` list:

```yaml
- id: my-area
  name: My Area
  description: What this group of repos is for
  items:
    - name: ...
```

The dashboard and architecture graph pick up new areas automatically.

### Statuses

| Status | Meaning |
|---|---|
| `active` | Actively maintained and used |
| `new` | Recently created, early stage |
| `experimental` | Proof of concept / research |
| `needs-decision` | Active but ownership or future unclear |
| `inactive` | Dead or abandoned |
| `unknown` | Needs investigation |

## Features

- **Inventory tab** — searchable, filterable list of all items grouped by area. Click status chips to filter.
- **Architecture tab** — dependency graph showing relationships between items. Click a node to highlight its connections. Drag nodes to rearrange. Scroll to zoom.
- **Machine-readable** — the YAML file can be parsed directly by AI tools or scripts.

## Files

| File | Purpose |
|---|---|
| `felt-platform-inventory.yaml` | Source of truth — edit this |
| `index.html` | Dashboard viewer (served by GitHub Pages) |
