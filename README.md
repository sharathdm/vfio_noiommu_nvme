# vfio_noiommu_nvme

boot linux with huge pages "default_hugepagesz=1G hugepagesz=1G hugepages=1"

root@root:~#

root@root:~# cat /sys/module/vfio/parameters/enable_unsafe_noiommu_mode

N

root@root:~# echo 1 > /sys/module/vfio/parameters/enable_unsafe_noiommu_mode

root@root:~# cat /sys/module/vfio/parameters/enable_unsafe_noiommu_mode

Y

root@root:~# rmmod nvme

root@root:~# echo 0000:03:00.0 > /sys/bus/pci/devices/0000:03:00.0/driver/unbind

-bash: /sys/bus/pci/devices/0000:03:00.0/driver/unbind: No such file or directory

root@root:~# echo 144d a808 > /sys/bus/pci/drivers/vfio-pci/new_id

root@root:~# lspci -vv -s 03:00.0

03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983 (prog-if 02 [NVM Express])

        Subsystem: Samsung Electronics Co Ltd SSD 970 EVO Plus 1TB

        Control: I/O- Mem+ BusMaster- SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-

        Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-

        Interrupt: pin A routed to IRQ 16

        NUMA node: 0

        IOMMU group: 0

        Region 0: Memory at 4b200000 (64-bit, non-prefetchable) [size=16K]

        Capabilities: [40] Power Management version 3

                Flags: PMEClk- DSI- D1- D2- AuxCurrent=0mA PME(D0-,D1-,D2-,D3hot-,D3cold-)

                Status: D3 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-

        Capabilities: [50] MSI: Enable- Count=1/1 Maskable- 64bit+

                Address: 0000000000000000  Data: 0000

        Capabilities: [70] Express (v2) Endpoint, MSI 00

                DevCap: MaxPayload 256 bytes, PhantFunc 0, Latency L0s unlimited, L1 unlimited

                        ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset+ SlotPowerLimit 25.000W

                DevCtl: CorrErr- NonFatalErr- FatalErr- UnsupReq-

                        RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop+ FLReset-

                        MaxPayload 256 bytes, MaxReadReq 512 bytes

                DevSta: CorrErr- NonFatalErr- FatalErr- UnsupReq- AuxPwr- TransPend-

                LnkCap: Port #0, Speed 8GT/s, Width x4, ASPM L1, Exit Latency L1 <64us

                        ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp+

                LnkCtl: ASPM Disabled; RCB 64 bytes, Disabled- CommClk+

                        ExtSynch- ClockPM+ AutWidDis- BWInt- AutBWInt-

                LnkSta: Speed 8GT/s (ok), Width x4 (ok)

                        TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-

                DevCap2: Completion Timeout: Range ABCD, TimeoutDis+ NROPrPrP- LTR+

                         10BitTagComp- 10BitTagReq- OBFF Not Supported, ExtFmt- EETLPPrefix-

                         EmergencyPowerReduction Not Supported, EmergencyPowerReductionInit-

                         FRS- TPHComp- ExtTPHComp-

                         AtomicOpsCap: 32bit- 64bit- 128bitCAS-

                DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis- LTR+ OBFF Disabled,

                         AtomicOpsCtl: ReqEn-

                LnkCap2: Supported Link Speeds: 2.5-8GT/s, Crosslink- Retimer- 2Retimers- DRS-

                LnkCtl2: Target Link Speed: 8GT/s, EnterCompliance- SpeedDis-

                         Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-

                         Compliance De-emphasis: -6dB

                LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete+ EqualizationPhase1+

                         EqualizationPhase2+ EqualizationPhase3+ LinkEqualizationRequest-

                         Retimer- 2Retimers- CrosslinkRes: unsupported

        Capabilities: [b0] MSI-X: Enable- Count=33 Masked-

                Vector table: BAR=0 offset=00003000

                PBA: BAR=0 offset=00002000

        Capabilities: [100 v2] Advanced Error Reporting

                UESta:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-

                UEMsk:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-

                UESvrt: DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-

                CESta:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr-

                CEMsk:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr+

                AERCap: First Error Pointer: 00, ECRCGenCap+ ECRCGenEn- ECRCChkCap+ ECRCChkEn-

                        MultHdrRecCap+ MultHdrRecEn- TLPPfxPres- HdrLogCap-

                HeaderLog: 00000000 00000000 00000000 00000000

        Capabilities: [148 v1] Device Serial Number 00-00-00-00-00-00-00-00

        Capabilities: [158 v1] Power Budgeting <?>

        Capabilities: [168 v1] Secondary PCI Express

                LnkCtl3: LnkEquIntrruptEn- PerformEqu-

                LaneErrStat: 0

        Capabilities: [188 v1] Latency Tolerance Reporting

                Max snoop latency: 3145728ns

                Max no snoop latency: 3145728ns

        Capabilities: [190 v1] L1 PM Substates

                L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+

                          PortCommonModeRestoreTime=10us PortTPowerOnTime=10us

                L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-

                           T_CommonMode=0us LTR1.2_Threshold=81920ns

                L1SubCtl2: T_PwrOn=10us

        Kernel driver in use: vfio-pci

        Kernel modules: nvme

 

root@root:~# ls /dev/vfio/

noiommu-0  vfio

root@root:~# ls /dev/vfio/

noiommu-0  vfio

root@root:~#

root@root:~# ./a.out

Group fd = 4

20 3 9 5 0

region index =0

40 f 0 0 4000 0

region index =1

32 0 1 0 0 10000000000

region index =2

32 0 2 0 0 20000000000

region index =3

32 0 3 0 0 30000000000

region index =4

32 0 4 0 0 40000000000

region index =5

32 0 5 0 0 50000000000

region index =6

32 0 6 0 0 60000000000

region index =7

32 3 7 0 1000 70000000000

region index =8

32 0 8 0 0 0

irq index =0

16 7 0 1

irq index =1

16 9 1 1

irq index =2

16 9 2 33

irq index =3

16 9 3 1

irq index =4

16 9 4 1

Fd = 5

VFIO_GROUP_GET_DEV_ID = 15210

 

dump configuration space registers

a808144d

100002

1080200

10

4b200004

0

0

0

0

0

 

dump BAR0 space registers

3c033fff

30

10300

0

0

0

0

0

0

1f001f

1396a000

1

13969000

1

0

0

0

buffer addr 7ff580000000

VIRT 7ff580000000 7ff580004000 7ff580008000 7ff580009000 7ff58000d000

phy = 8180000001fc0000

phy = 8180000001fc0004

phy = 8180000001fc0008

phy = 8180000001fc0009

phy = 8180000001fc000d

PHYSICAL 1fc0000000 1fc0004000 1fc0008000 1fc0009000 1fc000d000

CC 6de740

CSTS 1

 

dump BAR0 space registers

3c033fff

30

10300

0

0

460001

0

1

0

1f001f

c0000000

1f

c0004000

1f

0

0

0

Enable MSIX Interrupts

identify controller

inside intr_thread_main

COMPLETION 0 0 1 11234

VID 14 4d

SSVID 14 4d

IEE 0 25 38

MTDS 9

SQES 66

CQES 44

NN 0 0 0 1

C_DB 1

 

identify namespace

COMPLETION 0 0 2 155aa

NSZE 0 0 0 0 1d 1c 59 70

NCAP 0 0 0 0 1d 1c 59 70

NUSE 0 0 0 0 6 fc 4 38

NLBAF 0

FLBAS 0

EUI 10 49 50 91 56 38 25 0

LBA format-0 0 9 0 0

LBA format-1 0 0 0 0

LBA format-2 0 0 0 0

C_DB 2

 

create io completion queue

COMPLETION 0 0 3 11234

C_DB 3

 

create io submission queue

COMPLETION 0 0 4 14321

C_DB 4

 

read block

INTR bytes_read = 8

COMPLETION 0 0 10001 1dada

C_DB_Q1 1

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 bb e2 ff 14 0 0 0 0

0 0 ee 0 0 0 1 0 0 0 ff 7 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 0 0 0 0 55 aa
