# Contributing

## Key directories
`_docs/` - directory containing documentation pages (in markdown) and file templates.

`_data/` - configuration files for the website. Only edit `/_data/sidebars/sidebar_ioos.yml`

`theme/` - **Do not edit** - the Jekyll theme files containing the look and feel and functionality of the site - sourced from the 
[ioos/documentation-theme-jekyll](https://github.com/ioos/documentation-theme-jekyll) repo.

# File Template Development
## Process
Below are the steps by which a team can iterate on developing a netCDF template.

1. Generate a [CDL](#cdl) file representing the netCDF file contents.
   1. File names should include a reference to the template type.
1. Submit the CDL as a Pull Request to this repository `_docs/data/templates`.
1. Review CDL
1. Raise issues by selecting the three dots on the line of concern and click "Reference in new issue". Include a description as to what should be changed.
1. Resolve issues by making the adjustment per the discussion in the issue and submitting a Pull Request via GitHub.
1. Once the template is finalized, a documentation site should be populated with details on the contents of the template.
1. Once the website is updated, create a [release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) of the repository.
   1. Use a tag that is logical for the release. Typically a [semantic version number](https://semver.org/) makes sense.   

## CDL
* CDL is a Common Data Language (CDL) text representation of a netCDF file, following the specifications provided [here](https://docs.unidata.ucar.edu/nug/current/_c_d_l.html).
* CDL can be generated from a netCDF file by using the `ncdump` [tool](https://www.unidata.ucar.edu/software/netcdf/workshops/2011/utilities/Ncdump.html), or various other tools.
* CDL can be used to generate a netCDF file using the `ncgen` [tool](https://linux.die.net/man/1/ncgen).
* An example working with a CDL file in python can be found in [this notebook](https://github.com/ioos/ioos-atn-data/blob/gh-pages/_docs/notebooks/create_atn_trajectory_template.ipynb)
* A CDL file can be edited using a simple text editor (like notepad, vim, emacs, or through the GitHub interface).

## Where to contribute
* Template files are found at `_docs/data/templates`.

# Website
## How to Contribute
The easiest way to get started is to file an issue to tell us about a spelling mistake, some awkward wording,
or a factual error. This is a good way to introduce yourself and to meet some of our community members.

1. If you have a [GitHub][github] account, or are willing to [create one][github-join], but do not know how to use Git,
you can report problems or suggest improvements by [creating an issue][issues]. This allows us to assign the item 
to someone and to respond to it in a threaded discussion.

2. If you are comfortable with Git, and would like to add or change material, you can submit a pull request (PR).
Instructions for doing this are [included below](#using-github).

## Where to Contribute
Contribute your documentation to the `_docs/` directory.

1. Update an existing page.
2. Create a new page.

## Using GitHub

If you choose to contribute via GitHub, you may want to look at [How to Contribute to an Open Source Project on 
GitHub][how-contribute]. To manage changes, we follow [GitHub flow][github-flow]. To use the web interface for contributing to a file:

1. Fork the originating repository to your GitHub profile.
2. Within your version of the forked repository, move to the `gh-pages` branch.
3. Navigate to the file(s) you wish to change within the branch and make revisions as required.
4. Commit all changed files within the appropriate branch.
5. Create pull requests from your changed branch to the `gh-pages` branch within the originating 
repository.
6. If you receive feedback, make changes using your issue-specific branches of the forked repository and the pull 
requests will update automatically.
7. Repeat as needed until all feedback has been addressed.

When starting work, please make sure your clone of the originating `gh-pages` branch is up-to-date before creating your own 
revision-specific branch(es) from there.

[github]: https://github.com
[github-flow]: https://guides.github.com/introduction/flow/
[github-join]: https://github.com/join
[how-contribute]: https://app.egghead.io/playlists/how-to-contribute-to-an-open-source-project-on-github
[issues]: https://guides.github.com/features/issues/

## Deploying site locally
Requirements:
* bundle
* Jekyll

See [IOOS How To: Local Development with Jekyll](https://ioos.github.io/ioos-documentation-jekyll-skeleton/howto.html#local-development-with-jekyll).

Clone this repository:
```commandline
git clone https://github.com/ioos/ncei-archiving-cookbook.git
```
Checkout the gh-pages branch:
```commandline
git checkout gh-pages
```
To build the site, in the `ncei-archiving-cookbook/` directory run:
```commandline
bundle exec jekyll serve --config _config.yml --watch --verbose --incremental
```
This will deploy a website at: http://127.0.0.1:4000/ncei-archiving-cookbook/

Make edits to the appropriate markdown files in `_docs/`. 

If changing headers and menus, stop the running server by entering `ctrl-c` in the terminal. Then run:
```commandline
bundle exec jekyll clean
```
Then build the site again.
```commandline
bundle exec jekyll serve --config _config.yml --watch --verbose --incremental
```
And review at http://127.0.0.1:4000/ioos-atn-data/
