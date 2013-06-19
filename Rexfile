use Rex::Lang::Perl::Perlbrew;
use Rex::Commands::Rsync;

die "No environment set." unless $ENV{BLAGGER_USER};

set perlbrew => root => "/home/$ENV{BLAGGER_USER}/perl5/perlbrew";

user $ENV{BLAGGER_USER};

group webserver => $ENV{BLAGGER_SERVER};

desc "Update blagger from git repo";
task "upgrade",
  group => "webserver",
  sub {
    perlbrew -use => "perl-5.16.3";
    say "Git update";
    run "cd /home/$ENV{BLAGGER_USER}/ztunzeed && git pull";
    say "cpan update";
    run
      "cd /home/$ENV{BLAGGER_USER}/ztunzeed && cpanm -q --notest --installdeps .";
    run "cd /home/$ENV{BLAGGER_USER}/ztunzeed && dzil install";
    say "Restarting blog";
    run "ubic restart stokesblog";
  };

desc "Sync posts";
task "deploy",
  group => 'webserver',
  sub {
    sync "posts/*", "/home/$ENV{BLAGGER_USER}/ztunzeed/posts",
      {parameters => '--delete',};
  };
