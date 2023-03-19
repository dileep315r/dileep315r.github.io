MISCELLANEOUS

grep -ri "de.groupon.logic.paymentprovider.PaymentProviderManagement" *
sh recreateDB.sh -d stardeals_it -h localhost -p 5432 -u postgres -V DETECT -v LATEST -s LATEST -b false
list only files  "ls -pR <directory>| grep -v /"


RUBYi

Sha1Hmac.new.compute_base64_hmac("dileep", "dileep is a good boy")

JIRA
project = "Tigers Android Consumer"  AND  creator = ckumarp ORDER BY created DESC
creator = kreddy ORDER BY created DESC
log format


GIT

git remote add -f b path/to/repo_b.git
git diff master remotes/b/master
git remote rm b

git diff --name-only
git rev-list --all | wc -l

make patches:
git format-patch -3 HEAD
git am < ~/Downloads/0002-changes-made-1.patch

apply git diff patch
If you want to create a patch file via "git diff" that can be applied using "patch -p0 < patchfile" use the following command:
git diff --no-prefix > patchfile
then apply the patch:
patch -p0 < patchfile
If you have an existing "git diff" patch file that was created without the "--no-prefix" option, you can apply that patch via:
patch -p1 < patchfile
this will ignore the default a/ b/ source prefixes.

rebase with remote copy:
git pull --rebase origin master


git reflog:
git reset --hard HEAD@{1}


Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author



rbenv commands:
rbenv version

gem env home

rbenv prefix 1.8.7-p357   --- get ruby installation directory

rbenv which irb


why to use scopes: aspiringwebdev.com/use-activerecord-scopes-not-class-methods-in-rails-to-avoid-errors/
nil problem: https://robots.thoughtbot.com/if-you-gaze-into-nil-nil-gazes-also-into-you


extract jar files
jar xf jar-file


Get process status information
cat /proc/pid/status


Exclude file from git
git rm --cached FILENAME
git config --global core.excludesfile ~/.gitignore


curl -H "Content-type: application/json" -H "Authorization:Token token=E7px6VVr3PVHZPJq51oa" -X GET -G --data-urlencode "status=triggered,acknowledged” "https://acme.pagerduty.com/api/v1/incidents"


Remove big file in git commits
git filter-branch --tree-filter 'rm -rf config/data/content_variant_service_production_requests_snc1_and_sac1_4.csv’ HEAD



IGNORE files
git status --porcelain | grep '^??' | cut -c4- >> .gitignore


Git explorer UI https://gitexplorer.com/




Command for monitoring system activity
Sar

Process run time
ps -o etime -p “28674"

Memory usage:
Proc /proc/meminfo

Bash force save a file
:w !sudo tee %

Rsync for efficient file sync
rsync -arvh $project_root_path/*  ft-gemino-gamma-eu-1c-f5f958d9.eu-west-1.amazon.com:/home/dileered/$project_dir_name/


Shell login scripts execution order https://shreevatsa.wordpress.com/2008/03/30/zshbash-startup-files-loading-order-bashrc-zshrc-etc/
TTY https://www.howtogeek.com/428174/what-is-a-tty-on-linux-and-how-to-use-the-tty-command/

Find process running on a port

lsof -nP -iTCP -sTCP:LISTEN | grep 5660



