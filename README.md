# wsg-assessment
A framework for doing assessments against the Web Sustainability Guidelines.

This tool generates a Markdown or CSV template document, with spaces next to each guideline to mark
a red/green/amber result, and a comment.

It also includes details of the exact version assessed against and the date the template was generated.

You can see an example of the Markdown output at https://manyfold.app/news/2024/07/12/wsg-assessment.html

## Requirements

Ruby 3.3

## Usage

rake generate:markdown

or

rake generate:csv
