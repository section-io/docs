---
title: View Varnish Cache Metrics
description: Guide for understanding Varnish Cache Counters and other Varnish Cache  metrics.
type: "docs"
keywords: varnish, Varnish Cache , cache, cached data, Varnish Cache counters, vcl, Varnish Cache configuration language, metrics
aliases:
  - /modules/varnish-cache/how-tos/varnish-metrics/
  - /varnish-metrics/
  - /reference/varnish-metrics/
  - /modules/varnish-cache/reference/varnish-metrics/

---

Out of the box, Section brings up Varnish Cache  metrics. The following is a description of these metrics.

## Varnish Cache Glossary

Key Varnish Cache concepts are described in the [Varnish Cache Glossary.]

## Varnish Cache Counters

Further detail with respect to key Varnish Cache Counters (Source; [Mankier])

### Counter Levels

Info- Informational counters  
Counters giving runtime information

Diag- Diagnostic counters  
Counters giving diagnostic information

Debug- Debug counters  
Counters giving Varnish Cache internals debug information

### Main Counters

sess\_conn  
Sessions accepted (INFO). Count of sessions successfully accepted

sess\_drop  
Sessions dropped (INFO).Count of sessions silently dropped due to lack of worker thread.

sess\_fail  
Session accept failures (INFO). Count of failures to accept TCP connection. Either the client changed its mind, or the kernel ran out of some resource like file descriptors.

sess\_pipe\_overflow  
Session pipe overflow (INFO). Count of sessions dropped due to the session pipe overflowing.

client\_req\_400  
Client requests received, subject to 400 errors (INFO). 400 means we couldn’’t make sense of the request, it was malformed in some drastic way.

client\_req\_411  
Client requests received, subject to 411 errors (INFO). 411 means the client did not send a Content-Length for the req.body.

client\_req\_413  
Client requests received, subject to 413 errors (INFO). 413 means that HTTP headers exceeded length or count limits.

client\_req\_417  
Client requests received, subject to 417 errors (INFO) 417 means that something went wrong with an Expect: header.

client\_req  
Good client requests received (INFO) The count of parseable client requests seen.

cache\_hit  
Cache hits (INFO) Count of cache hits. A cache hit indicates that an object has been delivered to a client without fetching it from a backend server.

cache\_hitpass  
Cache hits for pass (INFO) Count of hits for pass A cache hit for pass indicates that Varnish Cache is going to pass the request to the backend and this decision has been cached in it self. This counts how many times the cached decision is being used.

cache\_miss  
Cache misses (INFO) Count of misses A cache miss indicates the object was fetched from the backend before delivering it to the backend.

backend\_conn  
Backend conn. success (INFO) How many backend connections have successfully been established.

backend\_unhealthy  
Backend conn. not attempted (INFO)

backend\_busy  
Backend conn. too many (INFO)

backend\_fail  
Backend conn. failures (INFO)

backend\_reuse  
Backend conn. reuses (INFO) Count of backend connection reuses This counter is increased whenever we reuse a recycled connection.

backend\_toolate  
Backend conn. was closed (INFO)

backend\_recycle  
Backend conn. recycles (INFO) Count of backend connection recycles This counter is increased whenever we have a keep-alive connection that is put back into the pool of connections. It has not yet been used, but it might be, unless the backend closes it.

backend\_retry  
Backend conn. retry (INFO)

fetch\_head  
Fetch no body (HEAD) (INFO) beresp with no body because the request is HEAD.

fetch\_length  
Fetch with Length (INFO) beresp with Content-Length.

fetch\_chunked  
Fetch chunked (INFO) beresp with Chunked.

fetch\_eof  
Fetch EOF (INFO) beresp with EOF from lack of other info.

fetch\_bad  
Fetch bad T-E (INFO) beresp failed due to unknown Transfer-Encoding.

fetch\_close  
Fetch wanted close (INFO) beresp with EOF due to Connection: Close.

fetch\_oldhttp  
Fetch pre HTTP/1.1 closed (INFO) beresp with EOF due to HTTP &lt; 1.1

fetch\_zero  
Fetch zero len body (INFO) beresp with EOF due to keep-live but neither Chunked or Len.

fetch\_1xx  
Fetch no body (1xx) (INFO) beresp with no body because of 1XX response.

fetch\_204  
Fetch no body (204) (INFO) beresp with no body because of 204 response.

fetch\_304  
Fetch no body (304) (INFO) beresp with no body because of 304 response.

fetch\_failed  
Fetch failed (all causes) (INFO) beresp fetch failed.

fetch\_no\_thread  
Fetch failed (no thread) (INFO) beresp fetch failed, no thread available.

pools  
Number of thread pools (INFO) Number of thread pools. See also parameter thread\_pools. NB: Presently pools cannot be removed once created.

threads  
Total number of threads (INFO) Number of threads in all pools. See also parameters thread\_pools, thread\_pool\_min and thread\_pool\_max.

threads\_limited  
Threads hit max (INFO) Number of times more threads were needed, but limit was reached in a thread pool. See also parameter thread\_pool\_max.

threads\_created  
Threads created (INFO) Total number of threads created in all pools.

threads\_destroyed  
Threads destroyed (INFO) Total number of threads destroyed in all pools.

threads\_failed  
Thread creation failed (INFO) Number of times creating a thread failed. See VSL::Debug for diagnostics. See also parameter thread\_fail\_delay.

thread\_queue\_len  
Length of session queue (INFO) Length of session queue waiting for threads. NB: Only updates once per second. See also parameter queue\_max.

busy\_sleep  
Number of requests sent to sleep on busy objhdr (INFO) Number of requests sent to sleep without a worker thread because they found a busy object.

busy\_wakeup  
Number of requests woken after sleep on busy objhdr (INFO) Number of requests taken of the busy object sleep list and and rescheduled.

sess\_queued  
Sessions queued for thread (INFO) Number of times session was queued waiting for a thread. See also parameter queue\_max.

sess\_dropped  
sessions dropped for thread (INFO) Number of times session was dropped because the queue were too long already. See also parameter queue\_max.

n\_object  
object structs made (INFO) Number of object structs made

n\_vampireobject  
unresurrected objects (DIAG) Number of unresurrected objects

n\_objectcore  
objectcore structs made (INFO) Number of objectcore structs made

n\_objecthead  
objecthead structs made (INFO) Number of objecthead structs made

n\_waitinglist  
waitinglist structs made (DEBUG) Number of waitinglist structs made

n\_backend  
Number of backends (INFO) Number of backends known to us.

n\_expired  
Number of expired objects (INFO) Number of objects that expired from cache because of old age.

n\_lru\_nuked  
Number of LRU nuked objects (INFO) How many objects have been forcefully evicted from storage to make room for a new object.

n\_lru\_moved  
Number of LRU moved objects (DIAG) Number of move operations done on the LRU list.

losthdr  
HTTP header overflows (INFO)

s\_sess  
Total sessions seen (INFO)

s\_req  
Total requests seen (INFO)

s\_pipe  
Total pipe sessions seen (INFO)

s\_pass  
Total pass-ed requests seen (INFO)

s\_fetch  
Total backend fetches initiated (INFO)

s\_synth  
Total synthethic responses made (INFO)

s\_req\_hdrbytes  
Request header bytes (INFO) Total request header bytes received

s\_req\_bodybytes  
Request body bytes (INFO) Total request body bytes received

s\_resp\_hdrbytes  
Response header bytes (INFO) Total response header bytes transmitted

s\_resp\_bodybytes  
Response body bytes (INFO) Total response body bytes transmitted

s\_pipe\_hdrbytes  
Pipe request header bytes (INFO) Total request bytes received for piped sessions

s\_pipe\_in  
Piped bytes from client (INFO) Total number of bytes forwarded from clients in pipe sessions

s\_pipe\_out  
Piped bytes to client (INFO) Total number of bytes forwarded to clients in pipe sessions

sess\_closed  
Session Closed (INFO)

sess\_pipeline  
Session Pipeline (INFO)

sess\_readahead  
Session Read Ahead (INFO)

sess\_herd  
Session herd (DIAG)

shm\_records  
SHM records (DIAG)

shm\_writes  
SHM writes (DIAG)

shm\_flushes  
SHM flushes due to overflow (DIAG)

shm\_cont  
SHM MTX contention (DIAG)

shm\_cycles  
SHM cycles through buffer (DIAG)

sms\_nreq  
SMS allocator requests (DIAG)

sms\_nobj  
SMS outstanding allocations (DIAG)

sms\_nbytes  
SMS outstanding bytes (DIAG)

sms\_balloc  
SMS bytes allocated (DIAG)

sms\_bfree  
SMS bytes freed (DIAG)

backend\_req  
Backend requests made (INFO)

n\_vcl  
Number of loaded VCLs in total (INFO)

n\_vcl\_avail  
Number of VCLs available (DIAG)

n\_vcl\_discard  
Number of discarded VCLs (DIAG)

bans  
Count of bans (INFO) Number of all bans in system, including bans superseded by newer bans and bans already checked by the ban-lurker.

bans\_completed  
Number of bans marked ‘’completed’’ (DIAG) Number of bans which are no longer active, either because they got checked by the ban-lurker or superseded by newer identical bans.

bans\_obj  
Number of bans using obj.\* (DIAG) Number of bans which use obj.\* variables. These bans can possibly be washed by the ban-lurker.

bans\_req  
Number of bans using req.\* (DIAG) Number of bans which use req.\* variables. These bans can not be washed by the ban-lurker.

bans\_added  
Bans added (DIAG) Counter of bans added to ban list.

bans\_deleted  
Bans deleted (DIAG) Counter of bans deleted from ban list.

bans\_tested  
Bans tested against objects (lookup) (DIAG) Count of how many bans and objects have been tested against each other during hash lookup.

bans\_obj\_killed  
Objects killed by bans (lookup) (DIAG) Number of objects killed by bans during object lookup.

bans\_lurker\_tested  
Bans tested against objects (lurker) (DIAG) Count of how many bans and objects have been tested against each other by the ban-lurker.

bans\_tests\_tested  
Ban tests tested against objects (lookup) (DIAG) Count of how many tests and objects have been tested against each other during lookup. ‘’ban req.url == foo && req.http.host == bar’‘counts as one in’‘bans\_tested’‘and as two in’‘bans\_tests\_tested’’

bans\_lurker\_tests\_tested  
Ban tests tested against objects (lurker) (DIAG) Count of how many tests and objects have been tested against each other by the ban-lurker. ‘’ban req.url == foo && req.http.host == bar’‘counts as one in’‘bans\_tested’‘and as two in’‘bans\_tests\_tested’’

bans\_lurker\_obj\_killed  
Objects killed by bans (lurker) (DIAG) Number of objects killed by ban-lurker.

bans\_dups  
Bans superseded by other bans (DIAG) Count of bans replaced by later identical bans.

bans\_lurker\_contention  
Lurker gave way for lookup (DIAG) Number of times the ban-lurker had to wait for lookups.

bans\_persisted\_bytes  
Bytes used by the persisted ban lists (DIAG) Number of bytes used by the persisted ban lists.

bans\_persisted\_fragmentation  
Extra bytes in persisted ban lists due to fragmentation (DIAG) Number of extra bytes accumulated through dropped and completed bans in the persistent ban lists.

n\_purges  
Number of purge operations executed (INFO)

n\_obj\_purged  
Number of purged objects (INFO)

exp\_mailed  
Number of objects mailed to expiry thread (DIAG) Number of objects mailed to expiry thread for handling.

exp\_received  
Number of objects received by expiry thread (DIAG) Number of objects received by expiry thread for handling.

hcb\_nolock  
HCB Lookups without lock (DEBUG)

hcb\_lock  
HCB Lookups with lock (DEBUG)

hcb\_insert  
HCB Inserts (DEBUG)

esi\_errors  
ESI parse errors (unlock) (DIAG)

esi\_warnings  
ESI parse warnings (unlock) (DIAG)

vmods  
Loaded VMODs (INFO)

n\_gzip  
Gzip operations (INFO)

n\_gunzip  
Gunzip operations (INFO)

vsm\_free  
Free VSM space (DIAG) Number of bytes free in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

vsm\_used  
Used VSM space (DIAG) Number of bytes used in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

vsm\_cooling  
Cooling VSM space (DEBUG) Number of bytes which will soon (max 1 minute) be freed in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

vsm\_cooling  
Cooling VSM space (DEBUG) Number of bytes which will soon (max 1 minute) be freed in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

vsm\_overflow  
Overflow VSM space (DIAG) Number of bytes which does not fit in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

vsm\_overflowed  
Overflowed VSM space (DIAG) Total number of bytes which did not fit in the shared memory used to communicate with tools like varnishstat, varnishlog etc.

### Lock Counters

creat  
Created locks (DEBUG)

destroy  
Destroyed locks (DEBUG)

locks  
Lock Operations (DEBUG)

### Per Malloc Storage Counters

c\_req  
Allocator requests (INFO)

c\_fail  
Allocator failures (INFO)

c\_bytes  
bytes allocated (INFO)

c\_freed  
Bytes freed (INFO)

g\_alloc  
Allocations outstanding (INFO)

g\_bytes  
Bytes outstanding (INFO)

g\_space  
Bytes available (INFO)

### Per File Storage Counters

c\_req  
Allocator requests (INFO)

c\_fail  
Allocator failures (INFO)

c\_bytes  
Bytes allocated (INFO)

c\_freed  
Bytes freed (INFO)

g\_alloc  
Allocations outstanding (INFO)

g\_bytes  
Bytes outstanding (INFO)

g\_space  
Bytes available (INFO)

g\_smf  
N struct smf (INFO)

g\_smf\_frag  
N small free smf (INFO)

g\_smf\_large  
N large free smf (INFO)

### Per Backend Counters

vcls  
VCL references (DEBUG)

happy  
Happy health probes (INFO)

bereq\_hdrbytes  
Request header bytes (INFO) Total backend request header bytes sent

bereq\_bodybytes  
Request body bytes (INFO) Total backend request body bytes sent

beresp\_hdrbytes  
Response header bytes (INFO) Total backend response header bytes received

beresp\_bodybytes  
Response body bytes (INFO) Total backend response body bytes received

pipe\_hdrbytes  
Pipe request header bytes (INFO) Total request bytes sent for piped sessions

pipe\_out  
Piped bytes to backend (INFO) Total number of bytes forwarded to backend in pipe sessions

pipe\_in  
Piped bytes from backend (INFO) Total number of bytes forwarded from backend in pipe sessions

  [Varnish Cache Glossary.]: https://www.varnish-cache.org/docs/4.0/glossary/index.html
  [Mankier]: https://www.mankier.com/7/varnish-counters)
