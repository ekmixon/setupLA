#!/bin/bash
#  This script attempts to setup Linux Academy linux boxes for ansible
#   put passwords on user and root accounts
#   enable root login via ssh
#   Update everything
#   Install a repo containing ansible
#    etc...

#  Note: research "sshpass" to change passwords on new lab servers

# default "no" to all questions so <CR> will do nothing

DOMAIN="mylabserver.com"
HOST=$1.$DOMAIN


if [ "$1" == "" ]; then
  echo "usage: $0 <host>"
  echo " note: assumes DOMAIN=$DOMAIN"
  exit 1
fi

echo "Setting up lab server $HOST"
echo ""
echo "If this server is already configured"
echo "no need copy ssh keys to the server again"
echo ""

# List of things to be configured on a new server
# change user password
echo -n "Change password for user?"
read response
if [ "$response" == "y" ]
  then
    echo "  Changing user password"
    ssh user@$HOST passwd
fi

# NOTE: this will not work until ssh login as root has been enabled first
#echo -n "Change root password"
#read response
#if [ "response" == "y"]
# then
#   echo "Changing root password"
#fi

# enable root login via ssh
# Must change /etc/ssh/sshd_config AND RESTART SERVER!
# uncomment line "PermitRootLogin yes"
# then service sshd restart
echo -n "Copy ssh key to user? y|<cr>"
read response
if [ "$response" == "y" ]
 then 
   echo "  Copy ssh to user..."
   ssh-copy-id user@$HOST
fi

echo -n "Copy ssh key to root? y|<cr>"
read response
if [ "$response" == "y" ]
  then 
    echo "  Copy ssh key to root..."
    ssh-copy-id root@$HOST
fi

# exit 0  # exit for testing

# set root login true and restart ssh service
# ssh keys are there so lets use ssh
# add repo

echo -n "Add repo? y|<cr>"
read response
if [ "$response" == "y" ]
  then 
    echo "  Adding repo..."
    ssh root@$HOST yum -y install epel-release 
fi

# update system
echo -n "Start system update? y|<cr>"
read response
if [ "$response" == "y" ]
  then 
    echo "  Starting system update"
    ssh root@$HOST "yum -y update"
fi

# install ansible
echo -n "Install ansible? y|<cr>"
read response
if [ "$response" == "y" ]
  then 
    echo "  Installing ansible"
    ssh root@$HOST "yum -y install ansible"
fi
