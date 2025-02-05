# Disks

_Disks_ are virtual versions of physical storage devices, such as SSDs and HDDs.

Disks are designed for storing data and attach to VMs. Detaching a disk doesn't delete its data.

Each disk is located in an availability zone, where it's [replicated](#backup) to provide data protection. Disks are not replicated to other zones.

## Disks as a Yandex.Cloud resource {#disk-as-resource}

Disks are created in folders and inherit their access rights.

Disks take up storage space, which incurs additional fees. For more information, see [{#T}](../pricing.md). The size of a disk is specified during creation. This is the storage capacity that you're charged for.

If a disk is created from a snapshot or image, the disk information contains the ID of the source resource. In addition, the license IDs (`product_ids`) are inherited from the source resource, which are used to calculate the disk use cost.

## Disk types {#disks_types}

In Yandex.Cloud, there are two types of disks:

- Network SSD (`network-ssd`) — A fast network drive. Network block storage on an SSD.
- Network HDD (`network-hdd`) — A standard network drive. Network block storage on an HDD.

The availability zone affects which types of disks you can create.

## Attaching and detaching disks {#attach-detach}

Disks can only be attached to one VM at a time. The disk and VM must be located in the same availability zone.

VMs require one boot disk. Additional disks can also be attached.

{% include [attach-empty-disk](../_includes_service/attach-empty-disk.md) %}

When selecting a disk to attach to a VM, you can specify whether the disk should be deleted along with the VM. You can choose this option when creating a VM, updating it, or attaching a new disk to it.

If previously created disks are attached to the VM, they will be detached when the VM is deleted. Disk data is preserved and the disk can be attached to other VMs in the future.

If you want to delete a disk with a VM, specify this option during one of the following operations: when creating the VM, updating it, or attaching the disk to it. The disk will be deleted when you delete the VM.

**See also**

- Learn about [{#T}](../operations/vm-control/vm-attach-disk.md).
- Learn about [{#T}](../operations/vm-control/vm-detach-disk.md).

## Backups {#backup}

Each disk is automatically replicated in its availability zone.

As an additional backup, you can also create disk snapshots. Snapshots are automatically replicated to multiple availability zones. This lets you change the availability zone without losing any data.

If you often have to create a disk from its backup, you can create an image of the disk to speed up recovery. An example would be if you create a boot disk for your OS and want to install it on other VMs. Images are also automatically replicated to multiple availability zones.

## Read and write operations {#rw}

Disks and allocation units are subject to read and write operation limits. An allocation unit is a unit of disk space allocation, in GB. The allocation unit size depends on the [disk type](../concepts/limits.md#limits-disks).

The following maximum read and write operation parameters exist:

* Maximum IOPS: The maximum number of read and write operations performed by a disk per second.
* Maximum bandwidth: The total number of bytes that can be read from or written to a disk per second.

The actual IOPS value depends on the characteristics of the disk, total bandwidth, and the size of the request in bytes. Disk IOPS is determined by the following formula:

![image](../../_assets/compute/iops.svg)

For more information about maximum possible IOPS and bandwidth values, see [Quotas and limits](../concepts/limits.md#limits-disks).

### Disk performance {#performance}

To achieve the maximum possible IOPS, we recommend performing reads and writes that are 4 KB and less. Comparing to HDDs, SSDs have much higher IOPS for read operations, and lower operation latency values.

To achieve the maximum possible bandwidth, we recommend performing 4 MB reads and writes.

Disk performance depends on size: the more allocation units, the higher the IOPS and bandwidth values.

For small HDDs, there's a mechanism that raises their performance to that of 1 TB disks for peak loads. When a small disk works at the [basic performance level](../concepts/limits.md#limits-disks) for 12 hours, it accumulates "credits for operations". These are spent automatically when the load increases (for example, when a VM starts up). Small HDDs can work at increased performance for about 30 minutes a day. "Credits for operations" can be spent all at once or in small intervals.

