# Set up a Samba (SMB) server

## Prerequisites

Install the following packages:

```
samba
ntfs-3g
```

## Mount NTFS drive

An example fstab entry is:

```
/dev/sdd1	/data		ntfs-3g	rw,uid=1000,gid=1000,dmask=002,fmask=133	0	0
```

Once it's added to `/etc/fstab`:

```bash
systemctl daemon-reload
mount -a
```

## Set up Samba

Add a password to a user:

```
smbpasswd -a user
```
