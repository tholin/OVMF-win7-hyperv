# OVMF-win7-hyperv
A patched version of OVMF that works with hyperv in win7 guests

Windows 7 will fail to boot on OVMF if hyperv enlightenments and multicore are enabled. For full details see comment 7 on this bug.
[https://bugs.launchpad.net/qemu/+bug/1593605](https://bugs.launchpad.net/qemu/+bug/1593605)

This repo got a prebuilt 64-bit version of OVMF with the patch needed to make hyperv work.

    --- a/OvmfPkg/QemuVideoDxe/VbeShim.c
    +++ b/OvmfPkg/QemuVideoDxe/VbeShim.c
    @@ -87,7 +87,7 @@ InstallVbeShim (
       //
       Segment0Pages = 1;
       Int0x10       = (IVT_ENTRY *)(UINTN)Segment0 + 0x10;
    -  Status = gBS->AllocatePages (AllocateAddress, EfiBootServicesCode,
    +  Status = gBS->AllocatePages (AllocateAddress, EfiACPIMemoryNVS,
                       Segment0Pages, &Segment0);

       if (EFI_ERROR (Status)) {

Patch was applied and built from tianocore git repo on 170207.
[https://github.com/tianocore/edk2/tree/master/OvmfPkg](https://github.com/tianocore/edk2/tree/master/OvmfPkg)
