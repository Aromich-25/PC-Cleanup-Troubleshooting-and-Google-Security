@echo off
:: Disables the display of command lines during execution, keeping the script clean.

echo Deleting temporary files...
:: Deletes all files and directories in the %temp% folder (temporary files directory).
del /s /q %temp%\* & rmdir /s /q %temp%

echo Clearing prefetch files...
:: Deletes all files in the Windows Prefetch folder, which stores data to speed up application launches.
del /s /q C:\Windows\Prefetch\*

echo Clearing Windows Update cache...
:: Stops the Windows Update service to allow cache cleanup.
net stop wuauserv
:: Deletes all files in the SoftwareDistribution folder, which stores Windows Update files.
del /s /q C:\Windows\SoftwareDistribution\Download\*
:: Restarts the Windows Update service after cleanup.
net start wuauserv

echo Emptying Recycle Bin...
:: Removes all files in the Recycle Bin for all drives.
rd /s /q C:\$Recycle.Bin

echo Cleaning up disk...
:: Runs the Disk Cleanup tool with pre-configured cleanup settings (configured via cleanmgr /sageset).
cleanmgr /sagerun:1

echo Done!
:: Indicates the end of the script.
pause
:: Pauses the script to allow the user to see the output before closing the window.
