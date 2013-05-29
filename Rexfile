use Rex::Lang::Perl::Perlbrew;

set perlbrew => root => "/home/$ENV{BLAGGER_USER}/perl5/perlbrew";

user $ENV{BLAGGER_USER};

group webserver => $ENV{BLAGGER_SERVER};

desc "Update blagger from git repo";
task "deploy",
  group => "webserver",
  sub {
    perlbrew -use => "perl-5.16.3";
    say run "cpanm --notest --installdeps .";
    say run "cd /home/$ENV{BLAGGER_USER}/ztunzeed && git pull -q";
    say run "ubic restart stokesblog";
  };
