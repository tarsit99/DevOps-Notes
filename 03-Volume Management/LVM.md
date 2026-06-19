# Linux Volume Management & LVM

## ☁️ 1. Storage Basics & AWS EBS
*   **EBS (Elastic Block Storage):** Refers to external storage volumes. Storage consists of blocks, disks, and volumes.
*   **Device Names:** Root volumes are typically named `sd[a-e]`, while data volumes are named `sd[f-p]`. The root volume is configured while setting up the EC2 instance.
*   **Volume Attach vs. Volume Mount:** Volumes can be created and later attached. Attaching adds a block to the system, but mounting (binding) makes that block usable. We can mount in 2 types: LV mount and Disk mount.
*   **Essential Commands:**
    *   `$ lsblk`: Lists all the available disks or blocks that are attached to the EC2.
    *   `$ df -h`: Shows how much disk free space is available.

---

## 🧠 2. Traditional vs. Modern Storage (LVM)
*   **Traditional:** Attaching and mounting a single, static volume (e.g., taking a 10G volume and directly mounting it).
*   **Modern (DevOps):** Splitting a volume into multiple dynamic sections (e.g., taking a 10G volume and splitting it into 5G, 2G, and 3G) using Logical Volumes.
*   **What is LVM?** LVM (Logical Volume Manager) is a tool developed by canonical. It is a storage management system in Linux that allows you to create, resize, and manage disk space dynamically using PV, VG, and LV.
*   **Dynamic Storage Management:** The combination of cloud-level scalability (EBS) and OS-level flexibility (LVM) is used to dynamically manage storage.
*   **The Architecture Flow:** Disk -> Physical Volume (PV) -> Volume Group (VG) -> Logical Volume (LV).

---

## 🛠️ 3. Step-by-Step LVM Configuration
Before mounting, we have to make volumes into Physical Volumes (PV). Switch to the root user using `$ sudo su` and enter the `$ lvm` prompt.

### Step 1: Physical Volume (PV)
*   **Create PV:** `$ pvcreate /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1`.
*   **List PVs:** `$ pvs`.
*   **Show PV Info:** `$ pvdisplay`.

### Step 2: Volume Group (VG)
*   **Create VG:** `$ vgcreate tws_vg /dev/nvme1n1 /dev/nvme2n1` (where `tws_vg` is the volume group name).
*   **List VGs:** `$ vgs`.
*   **Show VG Info:** `$ vgdisplay`.

### Step 3: Logical Volume (LV)
*   **Create LV:** `$ lvcreate -L 10G -n tws_lv tws_vg`.
    *   *-L 10G*: Size flag.
    *   *-n tws_lv*: Logical Volume name.
    *   *tws_vg*: The Volume Group from which the LV is getting created.
*   **Show LV Info:** `$ lvdisplay`.

### Step 4: Format and Mount LV
*   **Create temporary mount point:** We need to create a mount location under a directory using `$ mkdir /mnt/tws_lv_mount`.
*   **Format the Logical Volume:** `$ mkfs.ext4 /dev/tws-vg/tws_lv`.
*   **Mount the LV:** `$ mount /dev/tws-vg/tws_lv /mnt/tws_lv_mount` (Source location -> Mount location). Now the disk or logical volume is reusable.

---

## 💽 4. Direct Disk Mounting (Manage AWS EBS)
If you don't want to use LVM and just want to mount a standard EBS disk:
1.  **Create mount point:** `$ mkdir /mnt/tws_disk_mount`.
2.  **Format the disk:** `$ mkfs -t ext4 /dev/nvme3n1`.
3.  **Mount the EBS:** `$ mount /dev/nvme3n1 /mnt/tws_disk_mount`.

---

## 📈 5. Extending & Unmounting Volumes
*   **Extend Logical Volume:** To dynamically extend the volume space (reflects on both `lsblk` & `df -h`), use the command: `$ lvextend -r -L +5G /dev/tws_vg/tws_lv`.
*   **Unmount Volume:** `$ umount /mnt/tws_lv_mount`.
    *   *Note:* Data won't loss if we unmount.
*   **(Bonus info):** `/etc/fstab` is utilized for standard filesystem table mounting.
