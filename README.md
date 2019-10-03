# vira

Vim JIRA interface plugin.

Stay inside vim while following and updating Jira issues
along with creating new issues on the go.

## Installation

Add to your Vim Plugins:

```
Plugin n0v1c3/vira
```

Install required python3 Jira package:
```
sudo python3 -m pip install jira
```

## Configuration

### Required

Add the following lines to your `$HOME/.vimrc` or `$HOME/.virarc`

```
let g:vira_srvs = ['https://jira.website.com', 'https://jira.othersite.com']
let g:vira_usrs = ['username_website', 'username_othersite']
let g:vira_pass = ['pass jira/website/n0v1c3', 'lpass show --password account']
```

These lists should be of equal length with at least **one** entry each
and represent the address of the JIRA site along with the user
names being used to log in.

Passwords are calls to external commands such as `pass` and `lpass`. If you do not
use software as mentioned you can remove the `g:vira_pass` variable and manually
enter the password when connecting. An `echo` could be used as a workaround in
the `g:vira_pass` however, this is not recommened for your security.

You will be propted for your password only **once for each vim session**
on the first usage.

### .virarc

The `.virarc` file(s) can be used to load the required settings for all
projects. Currently there will be a `.virarc` file searched for in user's
\$HOME directory along with the current `git` directory `root`.

These files are the recomended places for storing your custom
configurations. The default setting that you require saved in your
\$HOME directory and any project specific modifications.

Use a different filename:

```
let g:vira_virarc = '.virarc'
```

### Browser

The default browser used for :ViraBrowse is the environment variable \$BROWSER. Override this by setting g:vira_browser.

```
let g:vira_browser = 'chromium'
```

### TLS Certificate Verification

The following option can be set in order to connect to a sever that is using self-signed TLS certificates.

```
let g:vira_skip_cert_verify = 1
```

## Usage

A list of the important commands, functions and global variables
to be used to help configure Vira to work for you.

### Commands

- `ViraBrowse` - View Jira issue in web-browser.
- `ViraComment` - Insert a comment for active issue.
- `ViraEpics` - Get and Set Project(s) epic issues.
- `ViraFilterAssignees` - Add assignees to filter.
- `ViraFilterPriorities` - Add priorities to filter.
- `ViraFilterProjects` - Add projects to filter.
- `ViraFilterReset` - Reset filter to default.
- `ViraFilterStatuses` - Add statuses to filter.
- `ViraFilterTypes` - Add issuetypes to filter.
- `ViraIssue` - Create a new **issue**.
- `ViraIssues` - Get and Set the active **issue**.
- `ViraReport` - Get report for active issue.
- `ViraServers` - Get and Set active Jira server.
- `ViraTodo` - Make a **TODO** note for current issue.
- `ViraTodos `- Get a list of the remaining TODOs.

### Functions

- `ViraGetActiveIssue()` - Get the currently selected active issue.
- `ViraStatusline()` - Quick statusline drop-in.

### Variables

- `g:vira_null_issue` - Text used when there is no issue.
- `g:vira_null_project` - Text used when there is no project.

### Examples:

```
" Basics
nnoremap <silent> <leader>vI :ViraIssue<cr>
nnoremap <silent> <leader>vT :ViraTodo<cr>
nnoremap <silent> <leader>vb :ViraBrowse<cr>
nnoremap <silent> <leader>vc :ViraComment<cr>
nnoremap <silent> <leader>ve :ViraEpics<cr>
nnoremap <silent> <leader>vi :ViraIssues<cr>
nnoremap <silent> <leader>vr :ViraReport<cr>
nnoremap <silent> <leader>vs :ViraServers<cr>
nnoremap <silent> <leader>vt :ViraTodos<cr>

" Search filters
nnoremap <silent> <leader>vfP :ViraFilterPriorities<cr>
nnoremap <silent> <leader>vfa :ViraFilterAssignees<cr>
nnoremap <silent> <leader>vfp :ViraFilterProjects<cr>
nnoremap <silent> <leader>vfs :ViraFilterStatuses<cr>
nnoremap <silent> <leader>vft :ViraFilterReset<cr>
nnoremap <silent> <leader>vft :ViraFilterTypes<cr>

" Status
statusline+=%{ViraStatusline()}
```

### Plugin Support:

Plugins used and supported. This list will build as required
from other requests.

#### airline

_Full support planned_.

I am currently using the z section of airline until I figure
out the proper way to do it.

```
let g:airline_section_z = '%{ViraStatusLine()}'
```
