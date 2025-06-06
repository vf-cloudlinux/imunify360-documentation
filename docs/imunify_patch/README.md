# Imunify.Patch

## Introduction

Imunify.Patch is a tool designed to patch vulnerabilities in ImunifyAV(+) and Imunify360.

## Installation

TBD

## Licensing

Imunify.Patch requires a valid license key to be used. The license key can be obtained from the CloudLinux website via a link provided by Imunify360 plugin in your hosting panel web UI.



## Usage

### Usage from CLI

Imunify.Patch vulnerabilities scan for all users can be started with the following command:

```
$ imunify-antivirus malware scan user
```

Imunify.Patch vulnerabilities scan for a specific files path can be started with the following command:

```
$ imunify-antivirus malware on-demand queue put "/home/user1/*"
```

To see the list of vulnerabilities use following command:

```
$ imunify-antivirus vulnerabilities file list
```

Expected output should look like this:

```
APP_NAME   FILE_PATH                             ID  IMUNIFY_PATCH_USER_ID             PURCHASE_URL                                                                                                                                                                                       STATUS      SUBSCRIBED  USERNAME  VULNERABILITIES
WordPress  /home/user1/public_html/filename.php  1   35e75187d8ad4244bc5757edf26ed2b2  https://www.cloudlinux.com/purchase-imunify-patch?iaid=...&imunify_patch_user_id=...&server_ip=...&username=user1&websites=user1.com&total_websites=1&vulnerable_domains=1&vulnerabilities=%7B%7D  vulnerable  False       user1     [{'cve_id': '', 'vulnerability_type': 'XSS', 'vulnerability_description': 'XSS affecting the HTML API'}]
```

If you need to get JSON response, use the `--json` flag:

```
$ imunify-antivirus vulnerabilities file list --json
{"max_count": 1, "items": [{"id": 1, "username": "user1", "file_path": "/home/user1/public_html/wp-includes/html-api/class-wp-html-tag-processor.php", "status": "vulnerable", "app_name": "WordPress", "imunify_patch_user_id": "...", "subscribed": false, "purchase_url": "https://www.cloudlinux.com/purchase-imunify-patch?iaid=...&imunify_patch_user_id=...&server_ip=...&username=user1&websites=user1.com&total_websites=1&vulnerable_domains=1&vulnerabilities=%7B%7D", "vulnerabilities": [{"cve_id": "", "vulnerability_type": "XSS", "vulnerability_description": "XSS affecting the HTML API"}]}], "warnings": [], "version": "8.5.4", "eula": null, "license": {"status": true, "expiration": null, "user_limit": 2147483647, "id": "...", "user_count": 1, "message": "", "license_type": "imunifyAVPlus", "upgrade_url": "https://cln.cloudlinux.com/console/imunify360/servers/.../products/IMAVP/convert", "upgrade_url_360": "https://www.cloudlinux.com/upgrade-imunify-1/?iaid=...&users=1", "ip_license": false, "eligible_for_imunify_patch": false}}
```

To patch a specific file from the list of vulnerable files, use the `patch` command:

```
$ imunify-antivirus vulnerabilities file patch <path-to-file1> <path-to-file2> ...
```

where `<path-to-file1>` and `<path-to-file2>` are the paths to the files you want to patch.

for example:

```
$ imunify-antivirus vulnerabilities patch file /home/user1/public_html/wp-includes/html-api/class-wp-html-tag-processor.php
```

To restore original state of a patched file, use the `revert` command:

```
$ imunify-antivirus vulnerabilities file revert <path-to-file1> <path-to-file2> ...
```

where `<path-to-file1>` and `<path-to-file2>` are the paths to the files you want to restore.

for example:

```
$ imunify-antivirus vulnerabilities file revert /home/user1/public_html/wp-includes/html-api/class-wp-html-tag-processor.php
```
