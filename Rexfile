user $ENV{BLAGGER_USER};

group webserver => $ENV{BLAGGER_SERVER};

desc "Update blagger from git repo";
task "deploy", group => "webserver", sub {
     say run "cd /home/$ENV{BLAGGER_USER}/blagger && git pull -q";
     say run "ubic restart stokesblog";
};
