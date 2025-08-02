# webchanges-action
A GitHub Action to detect web page changes. It uses [mborsetti/webchanges](https://github.com/mborsetti/webchanges) to find differences between web pages.

## Usage

The following example workflow step will create an issue in a GitHub repository if a web page has changed.

```yml
- name: "Detect web page changes"
  id: webchanges
  uses: swimmwatch/webchanges-action@v1.0.1
  with:
    jobs: |
      name: Telegram Mini App documentation
      url: https://core.telegram.org/bots/webapps
      use_browser: false
      filters:
        - html2text
        - between:
            start: "#### __WebAppInitData"
            end: "#### __Events Available for Mini Apps"
    config: |
      report:
        tz: UTC
        github_issue:
          enabled: true
          owner: "${{ github.repository_owner }}"
          repo: "${{ github.event.repository.name }}"
          token: "${{ secrets.GITHUB_TOKEN }}"
          format_dt: "%Y-%m-%d"
          title: "Telegram Mini App documentation update: {dt}"
          assignees: 
            - "swimmwatch"
          format_content: |
            ```diff
            {content}
            ```

```

## Options
The following input variables options can/must be configured:

| Input variable | Necessity | Description                                    | Default |
|----------------|-----------|------------------------------------------------|---------|
| `jobs`         | Required  | List of jobs to run for web changes detection. |         |
| `config`       | Required  | Configuration for the web changes detector.    |         |


## Contributing
We love your input! We want to make contributing to this project as easy and transparent as possible, whether it's:
- Reporting a bug
- Discussing the current state of the code
- Submitting a fix
- Proposing new features

## License
webchanges-action is licensed under the [MIT License](LICENSE).