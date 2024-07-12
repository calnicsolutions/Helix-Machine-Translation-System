# Helix Machine Translation Systems

## About
Helix is a Machine Translation System developed by Calnic Solutions and incubated in TWFTW International to translate text for low digital resource languages in Relli & Lodhi among other languages of India. Its open system can be used to develop other language pairs by incorporating language specific database. Tested on the available corpus of the Bible, HELIX can also translate General Domain text.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Contact](#contact)

## Usage
Download or Clone system repository from git.
-----------------------------------------------------
Use below command to clone system setup from git repository.

git clone git@github.com:avinashksingh/Helix-Machine-Translation-System.git

## Installation

Below mentioned language system mainly installed and tested in Ubuntu Operating Systems.

Dependency Software Requirements:
Java, CRF++, DashboardTool

Install system dependencies one by one.
-----------------------------------------------------
Step 1: JAVA Installation
-----------------------------------------------------

Require Jdk 1.8 or higher, Download and copy it to /usr/local

sudo cp jdk-8u101-linux-x64.tar.gz /usr/local/

cd /usr/local/

Extract JAVA File

sudo tar -xvzf jdk-8u101-linux-x64.tar.gz

Open /etc/profile in vi editor

sudo vi /etc/profile

Inside VI Editor copy below two lines:

export JAVA_HOME=/usr/local/jdk1.8.0_101

export PATH=$JAVA_HOME/bin:$PATH

And past these lines at bottom (Below fi line) inside the VI Editor.

Save and quit the editor window.

Change to source mode:

source /etc/profile

Check JAVA Version

java -version


Step 2: Install Essential Files
-----------------------------------------------------
Install files.

sudo apt-get install build-essential

sudo apt-get install libgdbm-dev libglib2.0-dev


Step 3: CRF++ Installation
-----------------------------------------------------
Extract CRF++ File

tar -xvzf CRF++-0.58.tgz

Navigate to CRF ++ -0.58 folder

cd CRF++-0.58/

Use below four commands to install it.

Configure CRF++

./configure

make

sudo make install

Create a symbolic Link from the library file ‘/usr/local/lib/libcrfpp.so.0’ to 
‘/usr/lib/libcrfpp.so.0’.

sudo ln -s /usr/local/lib/libcrfpp.so.0 /usr/lib/libcrfpp.so.0

Test CRF++ Version.

crf_test --version


Step 4: Installation of Dashboard
-----------------------------------------------------
Extract Dashboard Files.

tar -xvzf DashboardTool-1.9.tgz

Navigate to Dashboard Tool-1.9

cd DashboardTool-1.9/

Print the list of directories where Perl searches for modules.

/usr/bin/perl -e 'print join "\n", @INC'

Display the contents of a file in the terminal.

cat Installation_Dash.sh

Open Installation_dash in VI editor.

vi Installation_Dash.sh

Inside VI Editor.

Hash First two lines:

#PERL=’perl -v 2>/dev/null’

#PERL_VER= ‘echo $PERL | awk ‘{ print substr($4, 2, 7);}’

Change 5.34 to 5.30 in 4th and 5th line and remove /.

Save and exit.

Install Dashboard.

sudo sh Installation_Dash.sh

Open Dashboard.

source /etc/profile

Dashboard.sh

Inside the Dashboard specify locations.

Set Dashboard path as:

/usr/share/Dashboard


Step 5: Hindi morph required only for Hindi analysis systems(i.e hin2lodhi, hin2mehra)
--------------------------------------------------------------------------------------
Extract hin-morph File.

tar -xvzf hin-morph.tgz

Navigate to the hin-morph directory.

cd hin-morph/

Create a new directory named mymorph.

mkdir mymorph

Assign the value to a new variable setu.

export setu=mymorph

Assign the values in the current directory to setu.

export setu=/home/calnic/sampark_files/hin-morph

Navigate to data_src/sl/morph/hin/

cd data_src/sl/morph/hin/shell/

Open the file create_dbm_dict.pl in VI editor.

vi create_dbm_dict.pl

Inside Hash Third line

#tie(%LEX,GDBM_FILE,$ARGV[0],&GDBM_WRCREAT,0644);

Add one line.

tie(%LEX,GDBM_File,$ARGV[0], &GDBM_WRCREAT, 0640) or die "Cannot open:$!\n";

Save and Exit.

Open the file create_dbm_suff.pl in VI editor.

vi create_dbm_suff.pl

Inside Hash Third line

#tie(%LEX,GDBM_FILE,$ARGV[1],0666,0);

Add one line.

tie(%LEX,GDBM_File,$ARGV[1], &GDBM_WRCREAT, 0640) or die "Cannot open:$!\n";

Save and Exit.

Open the file create_dbm_uword.pl in VI editor.

vi create_dbm_uword.pl

Inside Hash Third line

#tie(%LEX,GDBM_FILE,$ARGV[1],0666,0);

Add one line.

tie(%LEX,GDBM_File,$ARGV[1], &GDBM_WRCREAT, 0640) or die "Cannot open:$!\n";

Save and Exit

Navigate to src/sl/morph/hin/

cd src/sl/morph/hin/

Compile

make compile

Install

make install


Step 6: Install sampark-hin-lbm system(follow similar steps for hin2mehra 
and telugu2relli system installation)
-----------------------------------------------------

Extract sampark-hin-lbm-0.1.tgz
tar -xvzf sampark-hin-lbm-0.1.tgz

Navigate to home.

Create a symbolic link named "sampark" that points to the

"sampark-hin-lbm-0.1" directory.

ln -s sampark-hin-lbm-0.1 sampark

Open VI editor and edit the .bashrc file

vi .bashrc

Inside the editor add one line to the bottom of the page ie, below fi.

export setu=$HOME/sampark

Save and Quit.

Use source command.

source .bashrc

Display the value of the environment variable.

echo $setu

Open sampark/bin/sys/hin_tel/hin_tel_setu.spec in VI editor.

vi sampark/bin/sys/hin_tel/hin_tel_setu.spec

Inside the editor change the system name as your home directory.
Example:

<ENV>$setu=/home/trmt/sampark to

<ENV>$setu=/home/calnic/sampark

Also change the system name above “%SYSTEM%” code.

<OUTPUT_DIR>/home/trmt/OUTPUT.tmp to

<OUTPUT_DIR>/home/calnic/OUTPUT.tmp

Save and Exit.


Step 7: Final Steps(use this step only for hindi2lodhi and hindi2mehra system)
-----------------------------------------------------

Navigate to sampark/bin/sl/morph/

cd sampark/bin/sl/morph/

Rename hin to hin-old.

mv hin/ hin-old

Copy the contents to the current directory.

cp -r /home/calnic/hin-morph/bin/sl/morph/hin/ .

Navigate to Sampark.

Navigate to data_bin/sl/morph/

cd data_bin/sl/morph/

Rename hin to hin-old.

mv hin/ hin-old

Copy the contents to the current directory.

cp -r /home/calnic/hin-morph/data_bin/sl/morph/hin/ .

Navigate to Sampark.


Navigate to bin/sl/morph/hin.

cd bin/sl/morph/hin

Display the contents of a file in the terminal.

cat morph.sh

Run the "morph_run.sh" script

sh morph_run.sh tests/morph_test.in

This line shows an error. We have to correct it(We have python code errors and

have to correct all of them).

Open morph_run.sh in VI editor.

vi morph_run.sh

Inside, change python to python3.

Save and Exit.

Open morph.sh in IV editor.

vi morph.sh

Inside, change python to python3.

Save and Exit.

Open nukta-adder.py +47 in VI editor

vi nukta-adder.py +47

Change print i.strip(“\n”) to print(i.strip(“/n”))

Save and Exit.

Open nukta-adder.py +62 in VI editor.

vi nukta-adder.py +62

Change print arr[0]+”\t”+arr[1]+”\t”+arr[2]+”\t”+final_fs.rstrip(“|”) to

print(arr[0]+”\t”+arr[1]+”\t”+arr[2]+”\t”+final_fs.rstrip(“|”))

Save and Exit.

Open nukta-adder.py +64 in VI editor.

vi nukta-adder.py +64

Change print i.strip(“/n”) to print(i.strip(“/n”))

Save and Exit.

Run the "morph_run.sh" script

sh morph_run.sh tests/morph_test.in

Display the value of the environment variable.

echo $setu

Run the "morph.sh" script

sh morph.sh tests/morph_test.in

Step 8: Follow below steps to run the system
-----------------------------------------------------
perl /usr/share/Dashboard/source/dash.pl 
-c /home/calnic/sampark/bin/sys/hin_tel/hin_tel_setu.spec 
-i /home/calnic/sampark/bin/sl/morph/hin/tests/morph1.rin -l debug.log 
-o /home/calnic/OUTPUT.tmp

Note:- home, language pair and test files changes according to your requirement and
setup.

## Contact
jossy@calnicsolutions.com
