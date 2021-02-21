![Test](https://github.com/emmahsax/notify-slack-action/workflows/Test/badge.svg) ![Integration](https://github.com/emmahsax/notify-slack-action/workflows/Integration/badge.svg)

# Slack - GitHub Action

A [GitHub Action](https://github.com/features/actions) to send a message to a Slack channel that supports attachments like images.

## Archival Notice

This repository has been archived and designated as read-only. From GitHub's documentation:

> This will make the emmahsax/notify-slack-action repository, issues, pull requests, labels, milestones, projects, wiki, releases, commits, tags, branches, reactions and comments read-only and disable any future comments. The repository can still be forked.

For a similar GitHub Action that is _not_ archived, please visit the source of this project: https://github.com/cemkiy/action-slacker.

To unarchive this repository at any time, please reach out to me at https://emmasax.com/contact-me/.

## Configuration

You must set a Slack webhook environment value in settings page of your repository in order to use without any problem. Please [see here](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets#creating-encrypted-secrets) to learn how to do it if you don't know already.

## Usage

Create a workflow, set a step that uses this action and don't forget to specify the `slack_webhook` as a required variable.

```yaml
name: Notification on push

on:
  push:
    branches:
    - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Slack notification
      uses: emmahsax/notify-slack-action@main
      with:
        # requirements fields for slack
        slack_webhook: ${{ secrets.SLACK_WEBHOOK }}
        channel: '#channel-name'
        icon_url: 'slack user icon url'
        username: 'slack username'
        # attachment fields(not required)
        fallback: 'Required plain-text summary of the attachment.'
        color: '#36a64f'
        pretext: 'Optional text that appears above the attachment block'
        author_name: 'John Doe'
        author_link: 'http://jdoe.com/me/'
        author_icon: 'http://imageurl.com/icons/icon.jpg'
        title: 'Slack API Documentation'
        title_link: 'https://api.slack.com/'
        text: 'Optional text that appears within the attachment'
        image_url: 'http://my-website.com/path/to/image.jpg'
        thumb_url: 'http://example.com/path/to/thumb.png'
        footer: 'Slack API'
        footer_icon: 'https://platform.slack-edge.com/img/default_application_icon.png'
```

## Output

If you've set an attachment, only the attachment you provide will be sent to Slack. Otherwise, here's the default output if you've not set any attachment.

![Image of screenshot](https://raw.githubusercontent.com/cemkiy/action-slacker/master/screnshot.png)

## Advanced Usage

If you want to show different messages based on succes or failure of previous steps in your workflow, use success and failure functions.

```yaml
- name: Slack notification Failure
  if: failure()
  uses: emmahsax/notify-slack-action@main
  with:
    slack_webhook: ${{ secrets.SLACK_WEBHOOK }}
    channel: '#channel-name'
    icon_url: 'slack user icon url'
    username: 'slack username'
    image_url: 'http://my-website.com/path/to/failure.jpg'

- name: Slack notification Success
  if: success()
  uses: emmahsax/notify-slack-action@main
  with:
    slack_webhook: ${{ secrets.SLACK_WEBHOOK }}
    channel: '#channel-name'
    icon_url: 'slack user icon url'
    username: 'slack username'
    image_url: 'http://my-website.com/path/to/success.jpg'
```

## Contributing

Please see [API documentation](https://api.slack.com/docs/messages/builder) in addition to source code in this repository.

## License

[MIT](LICENSE) © 2019 Cem Kıy

## Does this interest you?

Join us at <a href="https://arge.biges.com/">Biges R&D</a> where we create software and hardware for physical security needs.
