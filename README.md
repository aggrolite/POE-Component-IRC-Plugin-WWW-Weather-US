# NAME

POE::Component::IRC::Plugin::WWW::Weather::US - IRC plugin to weather US weather by zip code

# SYNOPSIS

    use strict;
    use warnings;

    use POE qw(Component::IRC  Component::IRC::Plugin::WWW::Weather::US);

    my $irc = POE::Component::IRC->spawn(
        nick    => 'nickname',
        server  => 'irc.freenode.net',
        port    => 6667,
        ircname => 'ircname',
    );

    POE::Session->create(package_states => [main => [qw(_start irc_001)]]);

    $poe_kernel->run;

    sub _start {
        $irc->yield(register => 'all');

      $irc->plugin_add(Weather => POE::Component::IRC::Plugin::WWW::Weather::US->new);

        $irc->yield(connect => {});
    }

    sub irc_001 {
        $irc->yield(join => '#channel');
    }

# DESCRIPTION

type !weather 91202 to get the current weather for a location, currenly fetched from [http://forecast.weather.gov/zipcity.php](http://forecast.weather.gov/zipcity.php)

# AUTHOR

Curtis Brandt <curtis@cpan.org>

# COPYRIGHT

Copyright 2013- Curtis Brandt

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO
