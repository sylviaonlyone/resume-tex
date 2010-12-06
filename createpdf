#!/usr/bin/perl
use strict;

my $PROJECT_ROOT = "$ENV{'HOME'}/wa/github/resume-tex/";
my $SUFFIX = 'tex';
my $TMPDIR = './tmp';
my $PDFDIR = './pdf_repo';
my $MSG_HEAD = 'createpdf --->';
chomp(my $CURDIR = $ENV{'PWD'});
my $r = @ARGV;

# check the input argument
unless ($r != 1)
{
  # get the input file name
  chomp(my $filepath = @ARGV[0]);

  # test the suffix of file, which should be 'tex'
  $r = $filepath !~ /.*\.$SUFFIX/;
  unless ($r)
  {
    # extract target name
    $filepath =~ /(\/ | \.)?([\w]+)\.$SUFFIX/;
    my $target = $2;

    # set absolute path
    $filepath = ($filepath !~ /^\/.*/) ? ($CURDIR . '/' . $filepath) : $filepath;
    print "$MSG_HEAD full path:\t$filepath\n$MSG_HEAD target:\t\t$target\n";

    # test the current directory, and change it to PROJECT_HOME
    if ($CURDIR ne $PROJECT_ROOT)
    {
      chdir "$PROJECT_ROOT" or die "cannot chdir to $PROJECT_ROOT: $!";
    }

    # excute the shell command
    $r = system "latex -output-directory=$TMPDIR/ $filepath; dvipdf $TMPDIR/$target.dvi $TMPDIR/$target.pdf; mv $TMPDIR/$target.pdf $PDFDIR/;";
    $r ? print "$MSG_HEAD shell command failed!\n" : print "$MSG_HEAD success!\n";
  }
}
else
{
  $r++;
}

if ($r)
{
# when error display usage instruction
print ("=== Usage ===
/path/to/createpdf /path/to/my.tex
");
}
