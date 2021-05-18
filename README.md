# Simple EtherCAT Master for Simulink Desktop (Windows)

[![View Simple EtherCAT Master for Simulink Windows Desktop on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/77233-simple-ethercat-master-for-simulink-windows-desktop)

The example Simple EtherCAT Master Driver Block SFunctions for Simulink Desktop (Windows) shows basic usage of the Simple Open EtherCAT Master (SOEM) library by transferring 32 bytes of input and output PDO data with an EtherCAT Slave device. The example models are to be run in Normal or Accelerator mode on Windows Desktop. The first example model uses a self made real-time execution Sfunction block where sample time is synchronized based on the slave distributed clock. The second example model uses the real-time execution block of the Simulink Desktop Real-Time Toolbox, which is more accurate and robust, but does not sync with the slave distributed clock. Note that External mode is not supported. Both example models were tested to transfer/receive 32 bytes of PDO data with with an Hilscher NXHAT52-RTE slave running on a Raspberry Pi.

Prerequisites:
- Supported version of Microsoft Visual Studio + Windows SDK installed
- Pcap driver installed
    - WinPcap for Windows 7/8/8.1, see https://www.winpcap.org
    - Win10Pcap for Windows 10, see http://www.win10pcap.org
    - Npcap for Windows 10, see https://nmap.org/npcap/. During install select winpcap compatible mode.
    
Build/usage instructions:
1. Download SOEM library from https://github.com/OpenEtherCATsociety/SOEM, and unpack SOEM library to a subfolder called SOEM in the map of this simulink model.
2. Copy and rename pcap dll files, because the pcap dll files included in the Matlab installation do not work and causes a crash. 
    - Copy C:\Windows\System32\Packet.dll as Packet64.dll in the map of this simulink model.
    - Copy C:\Windows\System32\wpcap.dll as wpcap64.dll in the map of this simulink model.
3. Open Simulink model "simple_ethercat_master_dc.slx" or "simple_ethercat_master_sldrt.slx". 
    - The first model uses a self made real-time pacer where sample time is synchronized based on the slave distributed clock. 
    - The second model uses the real-time pacer of Simulink Desktop Real-Time Toolbox, which is more accurate and robust, but does not sync with the slave distributed clock.
    - Note that some Pcap drivers require Matlab/Simulink to be run in administrator mode to access ethernet device. This can be by right-click Matlab icon, and select run in administrator mode.
4. Open the EtherCAT Master block, and in the "Libraries" tab adjust the INC_PATHs and LIB_PATHs to the correct paths of the SOEM include folders and the Windows SDK library and include folders.
5. Build the SOEM_desktop or the SOEM_sldrt Sfunction to verify it successfully builds.
6. Run the models in Normal or Accelerator mode. External mode is not supported.
    - First run is likely to fail, because DeviceID parameter must be correctly set.
    - After first run, open diagnostics viewer and note the DeviceID Nr. related to your Ethernet device.
    - Update DeviceID in the parameters of the SOEM_desktop or the SOEM_sldrt Sfunction and run again.
