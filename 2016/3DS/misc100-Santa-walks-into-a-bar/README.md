Misc 100 - Santa walks into a bar

Script:
```perl
my $santa_id = '7ab7df3f4425f4c446ea4e5398da8847';

my $cmd = `zbarimg -q $santa_id.png`;
print "$santa_id.png: $cmd";

while ($cmd =~ m/in ([a-f,0-9]{32})/g) {
    $cmd = `zbarimg -q $1.png`;
    print "$1.png: $cmd";
}

print ">> Done!\n";
```

Run:
```
$ perl SantaBar.pl
```

Results:
```
..... cut .....
7273c3c00f289b4c0db7ca0079d3bece.png: QR-Code:Now I have Daniel in 14e48cd01bf67e441ba8f932b19ee702
14e48cd01bf67e441ba8f932b19ee702.png: QR-Code:Now I have Benjamin in 40b2765b63a4e50dc89e09c49c2e1c56
40b2765b63a4e50dc89e09c49c2e1c56.png: QR-Code:I almost forgot Yahir in 6d606ff8b95474100712d327666577e8
6d606ff8b95474100712d327666577e8.png: QR-Code:I almost forgot you in 3ab3b4b87d57315315cbb0259a262177
3ab3b4b87d57315315cbb0259a262177.png: QR-Code:Y0ur gift is in goo.gl/wFGwqO inugky3leb2gqzjanruw42yk
>> Done!
```

Get the flag at http://goo.gl/wFGwqO
