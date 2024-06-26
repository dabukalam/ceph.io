---
title: "v14.2.1 Nautilus released"
date: "2019-04-29"
author: "TheAnalyst"
tags:
  - "release"
  - "nautilus"
---

This is the first bug fix release of Ceph Nautilus release series. We recommend all nautilus users upgrade to this release. For upgrading from older releases of ceph, general guidelines for upgrade to nautilus must be followed [Upgrading from Mimic or Luminous](http://docs.ceph.com/master/releases/nautilus/#nautilus-old-upgrade).

## Notable Changes

- The default value for mon\_crush\_min\_required\_version has been changed from firefly to hammer, which means the cluster will issue a health warning if your CRUSH tunables are older than hammer. There is generally a small (but non-zero) amount of data that will move around by making the switch to hammer tunables; for more information, see [Tunables](../../rados/operations/crush-map/#crush-map-tunables).
    
    If possible, we recommend that you set the oldest allowed client to hammer or later. You can tell what the current oldest allowed client is with:
    
    ceph osd dump | min\_compat\_client
    
    If the current value is older than hammer, you can tell whether it is safe to make this change by verifying that there are no clients older than hammer current connected to the cluster with:
    
    ceph features
    
    The newer straw2 CRUSH bucket type was introduced in hammer, and ensuring that all clients are hammer or newer allows new features only supported for straw2 buckets to be used, including the crush-compat mode for the [Balancer](../../rados/operations/balancer/#balancer).
- Ceph now packages python bindings for python3.6 instead of python3.4, because EPEL7 recently switched from python3.4 to python3.6 as the native python3. see the [epel lists announcement](https://lists.fedoraproject.org/archives/list/epel-announce@lists.fedoraproject.org/message/EGUMKAIMPK2UD5VSHXM53BH2MBDGDWMO/) for more details on the background of this change.
    

## Known Issues

- Nautilus-based librbd clients cannot open images stored on pre-Luminous clusters

## Changelog

- mgr/dashboard: readonly user can’t see any pages ([issue#39240](http://tracker.ceph.com/issues/39240), [pr#27611](https://github.com/ceph/ceph/pull/27611), Stephan Müller)
- mgr/dashboard: Filter iSCSI target images based on required features ([issue#39002](http://tracker.ceph.com/issues/39002), [pr#27363](https://github.com/ceph/ceph/pull/27363), Ricardo Marques)
- common/blkdev: get\_device\_id: behave if model is lvm and id\_model\_enc isn’t there ([pr#27158](https://github.com/ceph/ceph/pull/27158), Sage Weil)
- common/config: parse –default-$option as a default value ([pr#27217](https://github.com/ceph/ceph/pull/27217), Sage Weil)
- core: Improvements to auto repair ([issue#38616](http://tracker.ceph.com/issues/38616), [pr#27220](https://github.com/ceph/ceph/pull/27220), xie xingguo, David Zafman)
- dashboard: NFS: failed to disable NFSv3 in export create ([issue#39104](http://tracker.ceph.com/issues/39104), [issue#38997](http://tracker.ceph.com/issues/38997), [pr#27368](https://github.com/ceph/ceph/pull/27368), Tiago Melo)
- doc/releases/nautilus: fix config update step ([pr#27502](https://github.com/ceph/ceph/pull/27502), Sage Weil)
- install-deps.sh: install ‘\*rpm-macros’ ([issue#39164](http://tracker.ceph.com/issues/39164), [pr#27544](https://github.com/ceph/ceph/pull/27544), Kefu Chai)
- mgr/dashboard add polish language ([issue#39052](http://tracker.ceph.com/issues/39052), [pr#27287](https://github.com/ceph/ceph/pull/27287), Sebastian Krah)
- mgr/dashboard/qa: Improve tasks.mgr.test\_dashboard.TestDashboard.test\_standby ([pr#27237](https://github.com/ceph/ceph/pull/27237), Volker Theile)
- mgr/dashboard: 1 osds exist in the crush map but not in the osdmap breaks OSD page ([issue#38885](http://tracker.ceph.com/issues/38885), [issue#36086](http://tracker.ceph.com/issues/36086), [pr#27543](https://github.com/ceph/ceph/pull/27543), Patrick Nawracay)
- mgr/dashboard: Adapt iSCSI overview page to make use of ceph-iscsi ([pr#27541](https://github.com/ceph/ceph/pull/27541), Ricardo Marques)
- mgr/dashboard: Add date range and log search functionality ([issue#37387](http://tracker.ceph.com/issues/37387), [issue#38878](http://tracker.ceph.com/issues/38878), [pr#27283](https://github.com/ceph/ceph/pull/27283), guodan1)
- mgr/dashboard: Add refresh interval to the dashboard landing page ([issue#26872](http://tracker.ceph.com/issues/26872), [issue#38988](http://tracker.ceph.com/issues/38988), [pr#27267](https://github.com/ceph/ceph/pull/27267), guodan1)
- mgr/dashboard: Add separate option to config SSL port ([issue#39001](http://tracker.ceph.com/issues/39001), [pr#27393](https://github.com/ceph/ceph/pull/27393), Volker Theile)
- mgr/dashboard: Added breadcrumb tests to NFS menu ([issue#38981](http://tracker.ceph.com/issues/38981), [pr#27589](https://github.com/ceph/ceph/pull/27589), Nathan Weinberg)
- mgr/dashboard: Back button component ([issue#39058](http://tracker.ceph.com/issues/39058), [pr#27405](https://github.com/ceph/ceph/pull/27405), Stephan Müller)
- mgr/dashboard: Cannot submit NFS export form when NFSv4 is not selected ([issue#39105](http://tracker.ceph.com/issues/39105), [issue#39063](http://tracker.ceph.com/issues/39063), [pr#27370](https://github.com/ceph/ceph/pull/27370), Tiago Melo)
- mgr/dashboard: Error creating NFS export without UDP ([issue#39107](http://tracker.ceph.com/issues/39107), [issue#39090](http://tracker.ceph.com/issues/39090), [pr#27372](https://github.com/ceph/ceph/pull/27372), Tiago Melo)
- mgr/dashboard: Error on iSCSI disk diff ([pr#27460](https://github.com/ceph/ceph/pull/27460), Ricardo Marques)
- mgr/dashboard: Fix env vars of run-tox.sh ([issue#38798](http://tracker.ceph.com/issues/38798), [issue#38864](http://tracker.ceph.com/issues/38864), [pr#27361](https://github.com/ceph/ceph/pull/27361), Patrick Nawracay)
- mgr/dashboard: Fixes tooltip behavior ([pr#27395](https://github.com/ceph/ceph/pull/27395), Stephan Müller)
- mgr/dashboard: FixtureHelper ([issue#39041](http://tracker.ceph.com/issues/39041), [pr#27398](https://github.com/ceph/ceph/pull/27398), Stephan Müller)
- mgr/dashboard: NFS Squash field should be required ([issue#39106](http://tracker.ceph.com/issues/39106), [issue#39064](http://tracker.ceph.com/issues/39064), [pr#27371](https://github.com/ceph/ceph/pull/27371), Tiago Melo)
- mgr/dashboard: PreventDefault isn’t working on 400 errors ([pr#27389](https://github.com/ceph/ceph/pull/27389), Stephan Müller)
- mgr/dashboard: Typo in “CephFS Name” field on NFS form ([issue#39067](http://tracker.ceph.com/issues/39067), [pr#27449](https://github.com/ceph/ceph/pull/27449), Tiago Melo)
- mgr/dashboard: dashboard giving 401 unauthorized ([issue#38871](http://tracker.ceph.com/issues/38871), [pr#27219](https://github.com/ceph/ceph/pull/27219), ming416)
- mgr/dashboard: fix sparkline component ([issue#38866](http://tracker.ceph.com/issues/38866), [pr#27260](https://github.com/ceph/ceph/pull/27260), Alfonso Martínez)
- mgr/dashboard: unify button/URL actions naming + bugfix (add whitelist to guard) ([issue#37337](http://tracker.ceph.com/issues/37337), [issue#39003](http://tracker.ceph.com/issues/39003), [pr#27492](https://github.com/ceph/ceph/pull/27492), Ernesto Puerta)
- mgr/dashboard: update vstart to use new ssl\_server\_port ([issue#39124](http://tracker.ceph.com/issues/39124), [pr#27394](https://github.com/ceph/ceph/pull/27394), Ernesto Puerta)
- mgr/deepsea: use ceph\_volume output in get\_inventory() ([issue#39083](http://tracker.ceph.com/issues/39083), [pr#27319](https://github.com/ceph/ceph/pull/27319), Tim Serong)
- mgr/diskprediction\_cloud: Correct base64 encode translate table ([pr#27167](https://github.com/ceph/ceph/pull/27167), Rick Chen)
- mgr/orchestrator: Add error handling to interface ([issue#38837](http://tracker.ceph.com/issues/38837), [pr#27095](https://github.com/ceph/ceph/pull/27095), Sebastian Wagner)
- mgr/pg\_autoscaler: add pg\_autoscale\_bias ([pr#27387](https://github.com/ceph/ceph/pull/27387), Sage Weil)
- mon/MonClient: do not dereference auth\_supported.end() ([pr#27215](https://github.com/ceph/ceph/pull/27215), Kefu Chai)
- mon/MonmapMonitor: clean up empty created stamp in monmap ([issue#39085](http://tracker.ceph.com/issues/39085), [pr#27399](https://github.com/ceph/ceph/pull/27399), Sage Weil)
- msg/async v2: make v2 work on rdma ([pr#27216](https://github.com/ceph/ceph/pull/27216), Jianpeng Ma)
- msg: default to debug\_ms=0 ([pr#27197](https://github.com/ceph/ceph/pull/27197), Sage Weil)
- osd: OSDMapRef access by multiple threads is unsafe ([pr#27402](https://github.com/ceph/ceph/pull/27402), Zengran Zhang, Kefu Chai)
- qa/valgrind ([pr#27320](https://github.com/ceph/ceph/pull/27320), Radoslaw Zarzynski)
- rook-ceph-system namespace hardcoded in the rook orchestrator ([issue#38799](http://tracker.ceph.com/issues/38799), [issue#39250](http://tracker.ceph.com/issues/39250), [pr#27496](https://github.com/ceph/ceph/pull/27496), Sebastian Wagner)
- rpm,cmake: use specified python3 version if any ([pr#27382](https://github.com/ceph/ceph/pull/27382), Kefu Chai)
- bluestore: ceph-bluestore-tool: bluefs-bdev-expand cmd might assert if no WAL is configured ([issue#39253](http://tracker.ceph.com/issues/39253), [pr#27523](https://github.com/ceph/ceph/pull/27523), Igor Fedotov)
- bluestore: os/bluestore: fix bitmap allocator issues ([pr#27139](https://github.com/ceph/ceph/pull/27139), Igor Fedotov)
- build/ops,rgw: rgw: build async scheduler only when beast is built ([pr#27191](https://github.com/ceph/ceph/pull/27191), Abhishek Lekshmanan)
- build/ops: build/ops: Running ceph under Pacemaker control not supported by SUSE Linux Enterprise ([issue#38862](http://tracker.ceph.com/issues/38862), [pr#27127](https://github.com/ceph/ceph/pull/27127), Nathan Cutler)
- build/ops: build/ops: ceph-mgr-diskprediction-local requires numpy and scipy on SUSE, but these packages do not exist on SUSE ([issue#38863](http://tracker.ceph.com/issues/38863), [pr#27125](https://github.com/ceph/ceph/pull/27125), Nathan Cutler)
- build/ops: cmake/FindRocksDB: fix IMPORTED\_LOCATION for ROCKSDB\_LIBRARIES ([issue#38993](http://tracker.ceph.com/issues/38993), [pr#27601](https://github.com/ceph/ceph/pull/27601), dudengke)
- build/ops: cmake: revert librados\_tp.so version from 3 to 2 ([issue#39291](http://tracker.ceph.com/issues/39291), [issue#39293](http://tracker.ceph.com/issues/39293), [pr#27597](https://github.com/ceph/ceph/pull/27597), Nathan Cutler)
- build/ops: qa,rpm,cmake: switch over to python3.6 ([issue#39236](http://tracker.ceph.com/issues/39236), [issue#39164](http://tracker.ceph.com/issues/39164), [pr#27505](https://github.com/ceph/ceph/pull/27505), Boris Ranto, Kefu Chai)
- cephfs: fs: we lack a feature bit for nautilus ([issue#39078](http://tracker.ceph.com/issues/39078), [issue#39187](http://tracker.ceph.com/issues/39187), [pr#27497](https://github.com/ceph/ceph/pull/27497), Patrick Donnelly)
- cephfs: ls -S command produces AttributeError: ‘str’ object has no attribute ‘decode’ ([pr#27531](https://github.com/ceph/ceph/pull/27531), Varsha Rao)
- cephfs: mds|kclient: MDS\_CLIENT\_LATE\_RELEASE warning caused by inline bug on RHEL 7.5 ([issue#39225](http://tracker.ceph.com/issues/39225), [pr#27500](https://github.com/ceph/ceph/pull/27500), “Yan, Zheng”)
- common,core: crush: various fixes for weight-sets, the osd\_crush\_update\_weight\_set option, and tests ([pr#27119](https://github.com/ceph/ceph/pull/27119), Sage Weil)
- core,mgr: mgr: autoscale down can lead to max\_pg\_per\_osd limit ([issue#39271](http://tracker.ceph.com/issues/39271), [issue#38786](http://tracker.ceph.com/issues/38786), [pr#27547](https://github.com/ceph/ceph/pull/27547), Sage Weil)
- core,mon: mon/Monitor.cc: print min\_mon\_release correctly ([pr#27168](https://github.com/ceph/ceph/pull/27168), Neha Ojha)
- core,tests: tests: osd-markdown.sh can fail with CLI\_DUP\_COMMAND=1 ([issue#38359](http://tracker.ceph.com/issues/38359), [issue#39275](http://tracker.ceph.com/issues/39275), [pr#27550](https://github.com/ceph/ceph/pull/27550), Sage Weil)
- core: Rook: Fix creation of Bluestore OSDs ([issue#39167](http://tracker.ceph.com/issues/39167), [issue#39062](http://tracker.ceph.com/issues/39062), [pr#27486](https://github.com/ceph/ceph/pull/27486), Sebastian Wagner)
- core: ceph-objectstore-tool: rename dump-import to dump-export ([issue#39325](http://tracker.ceph.com/issues/39325), [issue#39284](http://tracker.ceph.com/issues/39284), [pr#27610](https://github.com/ceph/ceph/pull/27610), David Zafman)
- core: common/blkdev: handle devices with ID\_MODEL as “LVM PV …” but valid ID\_MODEL\_ENC ([pr#27096](https://github.com/ceph/ceph/pull/27096), Sage Weil)
- core: common: fix deferred log starting ([pr#27388](https://github.com/ceph/ceph/pull/27388), Sage Weil, Jason Dillaman)
- core: crush/CrushCompiler: Fix \_\_replacement\_assert ([issue#39174](http://tracker.ceph.com/issues/39174), [pr#27620](https://github.com/ceph/ceph/pull/27620), Brad Hubbard)
- core: global: explicitly call out EIO events in crash dumps ([pr#27440](https://github.com/ceph/ceph/pull/27440), Sage Weil)
- core: log: log\_to\_file + –default-\* + fixes and improvements ([pr#27278](https://github.com/ceph/ceph/pull/27278), Sage Weil)
- core: mon/MgrStatMonitor: ensure only one copy of initial service map ([issue#38839](http://tracker.ceph.com/issues/38839), [pr#27116](https://github.com/ceph/ceph/pull/27116), Sage Weil)
- core: mon/OSDMonitor: allow ‘osd pool set pgp\_num\_actual’ ([pr#27060](https://github.com/ceph/ceph/pull/27060), Sage Weil)
- core: mon: make mon\_osd\_down\_out\_subtree\_limit update at runtime ([pr#27582](https://github.com/ceph/ceph/pull/27582), Sage Weil)
- core: mon: ok-to-stop commands for mon and mds ([pr#27347](https://github.com/ceph/ceph/pull/27347), Sage Weil)
- core: mon: quiet devname log noise ([pr#27314](https://github.com/ceph/ceph/pull/27314), Sage Weil)
- core: osd/OSDMap: add ‘zone’ to default crush map ([pr#27117](https://github.com/ceph/ceph/pull/27117), Sage Weil)
- core: osd/PGLog.h: print olog\_can\_rollback\_to before deciding to rollback ([issue#38906](http://tracker.ceph.com/issues/38906), [issue#38894](http://tracker.ceph.com/issues/38894), [pr#27302](https://github.com/ceph/ceph/pull/27302), Neha Ojha)
- core: osd/osd\_types: fix object\_stat\_sum\_t fast-path decode ([issue#39320](http://tracker.ceph.com/issues/39320), [issue#39281](http://tracker.ceph.com/issues/39281), [pr#27555](https://github.com/ceph/ceph/pull/27555), David Zafman)
- core: osd: backport recent upmap fixes ([issue#38860](http://tracker.ceph.com/issues/38860), [issue#38967](http://tracker.ceph.com/issues/38967), [issue#38897](http://tracker.ceph.com/issues/38897), [issue#38826](http://tracker.ceph.com/issues/38826), [pr#27225](https://github.com/ceph/ceph/pull/27225), huangjun, xie xingguo)
- core: osd: process\_copy\_chunk remove obc ref before pg unlock ([issue#38842](http://tracker.ceph.com/issues/38842), [issue#38973](http://tracker.ceph.com/issues/38973), [pr#27478](https://github.com/ceph/ceph/pull/27478), Zengran Zhang)
- doc: doc/orchestrator: Fix broken bullet points ([issue#39168](http://tracker.ceph.com/issues/39168), [pr#27487](https://github.com/ceph/ceph/pull/27487), Sebastian Wagner)
- doc: doc: Minor rados related documentation fixes ([issue#38896](http://tracker.ceph.com/issues/38896), [issue#38903](http://tracker.ceph.com/issues/38903), [pr#27189](https://github.com/ceph/ceph/pull/27189), David Zafman)
- doc: doc: rgw: Added library/package for Golang ([issue#38730](http://tracker.ceph.com/issues/38730), [issue#38867](http://tracker.ceph.com/issues/38867), [pr#27549](https://github.com/ceph/ceph/pull/27549), Irek Fasikhov)
- mgr: mgr/dashboard: Error on iSCSI target submission ([pr#27461](https://github.com/ceph/ceph/pull/27461), Ricardo Marques)
- mgr: ceph-mgr: ImportError: Interpreter change detected - this module can only be loaded into one interprer per process ([issue#38865](http://tracker.ceph.com/issues/38865), [pr#27128](https://github.com/ceph/ceph/pull/27128), Tim Serong)
- mgr: mgr/DaemonServer: handle\_conf\_change - fix broken locking ([issue#38964](http://tracker.ceph.com/issues/38964), [issue#38899](http://tracker.ceph.com/issues/38899), [pr#27454](https://github.com/ceph/ceph/pull/27454), xie xingguo)
- mgr: mgr/balancer: Python 3 compatibility fix ([issue#38831](http://tracker.ceph.com/issues/38831), [issue#38855](http://tracker.ceph.com/issues/38855), [pr#27227](https://github.com/ceph/ceph/pull/27227), Marius Schiffer)
- mgr: mgr/dashboard: Check if gateway is in use before allowing the deletion via iscsi-gateway-rm command ([pr#27457](https://github.com/ceph/ceph/pull/27457), Ricardo Marques)
- mgr: mgr/dashboard: Display the number of active sessions for each iSCSI target ([pr#27450](https://github.com/ceph/ceph/pull/27450), Ricardo Marques)
- mgr: mgr/devicehealth: Fix python 3 incompatiblity ([issue#38957](http://tracker.ceph.com/issues/38957), [issue#38939](http://tracker.ceph.com/issues/38939), [pr#27390](https://github.com/ceph/ceph/pull/27390), Marius Schiffer)
- mgr: mgr/telemetry: add report\_timestamp to sent reports ([pr#27701](https://github.com/ceph/ceph/pull/27701), Dan Mick)
- mgr: mgr/telemetry: use list; redact host; 24h default interval ([pr#27709](https://github.com/ceph/ceph/pull/27709), Sage Weil, Dan Mick)
- mgr: mgr: Configure Py root logger for Mgr modules ([issue#38969](http://tracker.ceph.com/issues/38969), [pr#27261](https://github.com/ceph/ceph/pull/27261), Volker Theile)
- mgr: mgr: Diskprediction unable to transfer data into the cloud server ([issue#38970](http://tracker.ceph.com/issues/38970), [pr#27240](https://github.com/ceph/ceph/pull/27240), Rick Chen)
- mon: mon: add cluster log to file option ([pr#27346](https://github.com/ceph/ceph/pull/27346), Sage Weil)
- rbd,tests: backport krbd discard qa fixes to nautilus ([issue#38861](http://tracker.ceph.com/issues/38861), [pr#27258](https://github.com/ceph/ceph/pull/27258), Ilya Dryomov)
- rbd,tests: backport krbd discard qa fixes to stable branches ([issue#38956](http://tracker.ceph.com/issues/38956), [pr#27239](https://github.com/ceph/ceph/pull/27239), Ilya Dryomov)
- rbd: librbd: ignore -EOPNOTSUPP errors when retrieving image group membership ([issue#38834](http://tracker.ceph.com/issues/38834), [pr#27080](https://github.com/ceph/ceph/pull/27080), Jason Dillaman)
- rbd: librbd: look for pool metadata in default namespace ([issue#38961](http://tracker.ceph.com/issues/38961), [pr#27423](https://github.com/ceph/ceph/pull/27423), Mykola Golub)
- rbd: librbd: trash move return EBUSY instead of EINVAL for migrating image ([issue#38968](http://tracker.ceph.com/issues/38968), [pr#27475](https://github.com/ceph/ceph/pull/27475), Mykola Golub)
- rbd: rbd: krbd: return -ETIMEDOUT in polling ([issue#38792](http://tracker.ceph.com/issues/38792), [issue#38977](http://tracker.ceph.com/issues/38977), [pr#27539](https://github.com/ceph/ceph/pull/27539), Dongsheng Yang)
- rgw: multisite: data sync loops back to the start of the datalog after reaching the end ([issue#39075](http://tracker.ceph.com/issues/39075), [issue#39033](http://tracker.ceph.com/issues/39033), [pr#27498](https://github.com/ceph/ceph/pull/27498), Casey Bodley)
- rgw: orphans find perf improvements ([issue#39181](http://tracker.ceph.com/issues/39181), [pr#27560](https://github.com/ceph/ceph/pull/27560), Abhishek Lekshmanan)
- rgw: rgw admin: disable stale instance deletion in multisite ([issue#39015](http://tracker.ceph.com/issues/39015), [pr#27602](https://github.com/ceph/ceph/pull/27602), Abhishek Lekshmanan)
- rgw: Adding tcp\_nodelay option to Beast ([issue#38926](http://tracker.ceph.com/issues/38926), [pr#27355](https://github.com/ceph/ceph/pull/27355), Or Friedmann)
- rgw: Fix S3 compatibility bug when CORS is not found ([issue#38923](http://tracker.ceph.com/issues/38923), [issue#37945](http://tracker.ceph.com/issues/37945), [pr#27331](https://github.com/ceph/ceph/pull/27331), Nick Janus)
- rgw: LC: handle resharded buckets ([pr#27559](https://github.com/ceph/ceph/pull/27559), Abhishek Lekshmanan)
- rgw: Make rgw admin ops api get user info consistent with the command line ([issue#39135](http://tracker.ceph.com/issues/39135), [pr#27501](https://github.com/ceph/ceph/pull/27501), Li Shuhao)
- rgw: don’t crash on missing /etc/mime.types ([issue#38921](http://tracker.ceph.com/issues/38921), [issue#38328](http://tracker.ceph.com/issues/38328), [pr#27329](https://github.com/ceph/ceph/pull/27329), Casey Bodley)
- rgw: don’t recalculate etags for slo/dlo ([pr#27561](https://github.com/ceph/ceph/pull/27561), Casey Bodley)
- rgw: fix RGWDeleteMultiObj::verify\_permission() ([issue#38980](http://tracker.ceph.com/issues/38980), [pr#27586](https://github.com/ceph/ceph/pull/27586), Irek Fasikhov)
- rgw: fix read not exists null version return wrong ([issue#38811](http://tracker.ceph.com/issues/38811), [issue#38909](http://tracker.ceph.com/issues/38909), [pr#27306](https://github.com/ceph/ceph/pull/27306), Tianshan Qu)
- rgw: ldap: fix early return in LDAPAuthEngine::init w/uri not empty() ([issue#38754](http://tracker.ceph.com/issues/38754), [pr#26972](https://github.com/ceph/ceph/pull/26972), Matt Benjamin)
- rgw: nfs: skip empty (non-POSIX) path segments ([issue#38744](http://tracker.ceph.com/issues/38744), [issue#38773](http://tracker.ceph.com/issues/38773), [pr#27208](https://github.com/ceph/ceph/pull/27208), Matt Benjamin)
- rgw: nfs: svc-enable RGWLib ([issue#38774](http://tracker.ceph.com/issues/38774), [pr#27232](https://github.com/ceph/ceph/pull/27232), Matt Benjamin)
- rgw: support delimiter longer then one symbol ([issue#38777](http://tracker.ceph.com/issues/38777), [pr#27548](https://github.com/ceph/ceph/pull/27548), Matt Benjamin)
- rgw: sse c fixes ([issue#38700](http://tracker.ceph.com/issues/38700), [pr#27296](https://github.com/ceph/ceph/pull/27296), Adam Kupczyk, Casey Bodley, Abhishek Lekshmanan)
