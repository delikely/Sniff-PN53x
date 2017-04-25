# Sniff-PN53x

Origin source:https://github.com/nfc-tools/dev-tools.

## Problem

 Running sniff-pn53x.sh shows "Could not find any reader, sorry".

## Fix
Auto add serial ID to DEVID.

Added codes as follow(line 88 to line 103).
```
# Delete ")"
DEVID=$(echo $DEVID|cut -d ')' -f1)
# Get serail id
serial_ID_List=$(lsusb|egrep "(Serial)"|cut -d ' ' -f6)
# Attach ID to DEVID
for ID in $serial_ID_List
do
	# To determine whether id already exists
    echo $DEVID | grep $ID > /dev/null
    if [ $? == 1  ]
    then
    	DEVID=${DEVID}"|"${ID}
    fi
done
DEVID=${DEVID}")"
```

## Useage

```
username@linux:~$ sudo bash sniff-pn53x.sh

```
 or
```
root@linux:~#:./sniff-pn53x.sh
```