Programming 400 - Fibonacci

Script:
```perl
#!/usr/bin/perl -w

use IO::Socket;
use bigint;

my $data = '';
my $nc = IO::Socket::INET->new(
    PeerAddr=>"54.175.35.248",
    PeerPort=>8000,
    Timeout=>10,
    Type=>SOCK_STREAM) or die $@;

$nc->autoflush(1);
if ($nc) {
    while (1) {
        my $recv = sysread($nc, $data, 768);
        print "\n$data";
        
        # start
        if ($data =~ /inform the number (.+?):/) {
            kirim($1);
        }

        # capture questions and send answer
        if ($data =~ /Stage (.+) -> N = (.+)/) {
            my $jawab = recursive($2);
            print ($jawab);
            kirim($jawab);
        }
        
        # error handling
        if ($recv == 0) {
            print "*** Bye!\n";
            exit(1);
        }
        if ($data =~ /Wrong/) {
            print "*** Salah!\n";
            exit(1);
        }
    }
}

# calculate recursive calls
sub recursive {
    my $n = $_[0] + 1; #oupss
    
    # fibonacci sequence
    my ($a, $b) = (0, 1);
    for (2..$n) {
        ($a, $b) = ($b, $a+$b);
    }
    
    # recursive calls formula
    my $calls = (2 * $b - 2);
    
    # get last 3 numbers
    $calls = $calls % 1000;
    
    return $calls;
}

sub kirim {
    my $msg = $_[0];
    print $nc "$msg\n";
}
```

Run:
```
$ perl solved_fibonacci.pl
```

Results:
```
..... cut .....
 [+] Stage 97 -> N = 357
     The answer is: 556
 [+] Correct!

 [+] Stage 98 -> N = 489
     The answer is: 388
 [+] Correct!

 [+] Stage 99 -> N = 268
     The answer is: 136
 [+] Correct!

 [+] Stage 100 -> N = 312
     The answer is: 64
 [+] Correct!

 [+] Congratulations, the flag is: 3DS{g00d4lgorithmsC4nSaveYourTime}

*** Bye!
```
