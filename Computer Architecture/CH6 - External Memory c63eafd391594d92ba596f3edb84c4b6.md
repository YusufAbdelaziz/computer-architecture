# CH6 - External Memory.

- Magnetic Disk
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled.png)
    
    - A magnetic disk is a non-magnetizable circular platter called the substrate, coated with magnetizable material. The circular platter is divided into rings called tracks that start from the center of the circular platter to the edges.
    - Each track is then divided into small sectors which is place to store data.
    - The head is like a pen that is used to write data on the magnetic disk.
    - You can’t let the head be too close from the surface of the magnetic disk because that might harm the head.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%201.png)
    
    - The previous figure shows a section of a track.
    - The c-shaped element is the head wrapped in a coil in which current moves such that a magnetic field is generated between the two edges of the C shape. The magnetic field’s direction depends upon the moving current direction. So the generated magnetic field magnetizes an element that is below the head. The previous process is the write mechanism.
    - The reading mechanism is the opposite, the head is placed on the elements from which we want to read data, and then the magnetized element induces a current inside the coil of the head.
    - Using a single head for reading and writing is inappropriate because that caused a misunderstanding while reading from an element.
    - So another head that is made from a variable resistance is used for the sake of reading data.
    - So the resistance head value changes depending on the pole of magnetization of the element.
- Data Organization and Formatting.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%202.png)
    
    - So the circular platter consists of tracks that are denoted as the white circular shape, each track is then divided into sectors like $S_1$ and so on.
    - Each track is separated from the other using the grey circle which called inter-track gap. Also, each sector is separated from the other by the light gray gap called inter-sector gap.
    - The separating sections that are used between tracks and sectors are useful in separating the magnetization between them.
    - The number of sectors in the external tracks is equal to the number of sectors in the internal tracks so that you don’t have to store a variable amount of sectors in each layer of tracks. The disadvantage that we’re not making use of the larger areas at the larger external tracks.
- Constant Angular Velocity (CAV) disk.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%203.png)
    
    - To read data from the CAV disk, we need two important pieces of information, the track number and the sector number.
    - There’s an issue in allocating data on a sector. Consider you want to write a 1 byte in a sector of size 4 byte, you have to allocate the whole sector so this means there’s a redundant space.
- Multiple Zone Recording.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%204.png)
    
- Formatting of Segate ST506.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%205.png)
    
    - The format of Segate ST506 starts with a gap then an ID field.
    - The ID field is then divided into fields which starts by a synchronization byte to determine the start of ID field, then the track number, head number, sector number, and CRC.
    - CRC stands for Cyclic Redundancy Check which is a group of bits used for error checking.
    - The data field consists of sync byte, data field, and CRC field.
    - The time required to find a data on a track or sector depends on the place of the head.
    
- Magnetic Disk Physical Characteristics.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%206.png)
    
    - Head Motion.
        - We have two choices, the first is a fixed head for each track, or a movable head.
        - The first choice is great in read/write operations, you only need to wait for the disk movement and one of the heads reads the correct data from the assigned track. This comes on the expense of cost. Manufacturing multiple heads is not easy.
        - Second choice is a movable head, but it’s required to be more intelligent at the way of writing data to the disk, such that we’re making the least amount of possible moves.
    - Disk Portability
        - Determines whether a disk is removable or not.
    - Sides.
        - We can make use of the two surfaces of the circular platter by writing on both sides.
        - But this might require another head, or a single head that is moving upwards and downwards.
        - So we’re doubling the storage size at the expense of the writing/reading speed.
        
    - Platters
        - You may use multiple platter but that would require two heads for each platter.
    - Head Mechanism.
        - **Contact** → Used with floppy disks in which the head contacts with the surface of the disk directly.
        - **Fixed Gap** → In this type, the head must be very close to the surface but the surface has to be very smooth so it doesn’t harm the head.
        - **Aerodynamic gap** → The disk is moving very quickly that the head looks like it’s flying. So the movement speed of the disk controls the closeness of the head.
        
- Multiple-Platter Disk / Cylinder.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%207.png)
    
    - There’s a new term that is introduced in the multiple-platter disk, which is the **cylinder**.
    - A cylinder is a collection of same tracks on different platters. So we can say cylinder number 10 is equivalent to all tracks with number 10 on each platter.
    - You can make use of the movement of each head synchronously. Say you want to store a program in track number 10, and the heads are moving towards that track, so should you store the remaining of the same program in another track on the same platter or you just go downwards to store it on the same track number but with another platter?
    - The latter solution makes use of the heads movement. All heads are pointing to the track number 10, so we don’t waste time on going to another track on the same platter to store the same program.
- Disk Performance Parameters (Speed).
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%208.png)
    
    - The transfer rate depends on the interface that is used to connect the disk to the motherboard. For example SATA 1, SATA 2, and SATA 3.
    - It also depends on the type of the hard disk.
    - Read about **Disk Performance Parameters** in Stallings to be able to solve the problems in the sheet.
- RAID.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%209.png)
    
    - Two main problems we face with hard disks are the speed and the safety.
    - Hard disks are slow but inexpensive. Also, your laptop may hit the ground which might harm the mechanical parts in the hard disk.
    - RAID was introduced to address these problems. RAID stands for **Redundant Array of Independent/Inexpensive Disks**.
    - It consists of 7 levels but they don’t represent a hierarchy which means that RAID 1 is not an improvement of RAID 2 and so on.
    - RAID 0.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2010.png)
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2011.png)
        
        - In this type, we have four physical disks.
        - Say you have a program that its size is 4 Kb, so you’re storing the first 1 kb in the first disk, the second 1 kb in the second disk and so on.
        - The user doesn’t see the distributed disks, these disks are represented as a single logical disk using an array management software.
        - An advantage of such representation is that **the speed is increased** as you’re writing or reading data parallelly or at the same time.
        - Safety is also increased such that if there’s a problem in one disk, other disks still store parts of the data, so that decreases the overall damage.
            
            ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2012.png)
            
    - RAID 1.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2013.png)
        
        - In this type, we have mirror disks that are used for the sake of making our data safe.
        - So data are written to both disks, the original and the mirrored disk and you can read from either disks.
        - A huge advantage is the safety, so if the original disk is damaged, you can simply replace it with a new disk and start copying the data exist in the mirror disk into the new disk.
        - But a disadvantage is that the writing speed is decreased because you now need to write data to both disks as well as the overall cost is doubled.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2014.png)
        
    - RAID 2.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2015.png)
        
        - The main idea of this type is that we’re using extra disks to store the hamming code error correction for restoring lost data.
        - So we may use RAID 0 with the first four disks, and the three remaining disks are responsible of storing the hamming code.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2016.png)
        
    - RAID 3.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2017.png)
        
        - So in this type, we’re using a single extra disk that is used to store the parity bit. This means that for every four bits stored in the four disks (RAID 0), we store a parity bit in the extra disk.
        - We can only detect the error, but correction is not possible with parity bits.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2018.png)
        
    - RAID 4.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2019.png)
        
        - RAID 4 is similar to RAID 3, but the data is not distributed between disks.
        - We still use a single disk for storing parity bits.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2020.png)
        
    - RAID 5.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2021.png)
        
        - A huge disadvantage in the previous two types is that if something happens to the disk that stores the parity disks, you cannot find errors in your data.
        - So in RAID 5, parity bits of data are distributed among all the disks.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2022.png)
        
    - RAID 6.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2023.png)
        
        - Same as RAID 5 but it uses two types of correction codes, the parity and the hamming codes.
        - The main disadvantage is that there’s a large space allocated to store the two types of error correction.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2024.png)
        
- Optical Storage CD-ROM.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2025.png)
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2026.png)
    
    - The CD-ROM consists of a single spiral track that is divided into sectors.
    - It’s suitable for sequential data as well as random data, but access time on random data is large compared to sequential data.
    - So it’s faster than the hard disk in reading sequential data as it only consists of single track, but relatively slower in reading random data.
    - When the laser beam is shed on a pit on the CD, the reflected light is then dispersed.
    - So the second figure illustrates how the reading process works with CD-ROM.
    - So if the reflected light is not dispersed which means it’s 100% reflected, then the photo-detector would read 1, otherwise it’d read 0.
    - Notice that we used a laser beam rather than a light beam because we can control the radius of the beam. Also, the laser beam is not dispersed when moving through the medium.
    - CD-ROM Drive Speeds
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2027.png)
        
        - A 1 second of audio takes 1.2 m on the track.
        - It’s was then noticed that 1 second takes 150 KB to be stored.
        - After that, other speeds are quoted as multiples of 150 KB/s.
        
    - CD-ROM Format.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2028.png)
        
        - This figure represents a single sector on a track.
        - The sync field consists of 4 leads and trailing bits and 10 bits that are set to 1 in the middle. This fields helps to locating the start of each sector.
        - The next 4 byte consists of 4 fields which mainly defines the minute and the second at which the audio is playing as well as defining the sector number and the mode type.
        - The next 2048 bytes are used to store data.
        - The last 288 bytes are EEC (Encoding Cyclic Code) that is used for error detection and correction.
        - In Mode 0, we’re using all fields for storing data which is quite useful in storing sequential data.
        - In Mode 1, we’re using data field and layered ECC field so we can store data and detect error. Having all the fields is important in case you’re storing data that shouldn’t be corrupted or multiple files in the CD-ROM. This means we need to know the sectors in which data is stored and their number.
        - In Mode 2, we’ve omitted the EEC field and combined it to the data field so to extend the storage space. This means that we don’t have the ability of detecting errors. Used with small audio or video files in which error correcting isn’t really critical but we can’t get rid of the ID field.
        
    - Random Access on CD-ROM
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2029.png)
        
    - Advantages and disadvantages of CD-ROM.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2030.png)
        
    - Types of CD ROM.
        - The first type is CD-ROM that is used just to read from it. Like windows CD-ROMs.
        - The second type is recordable CD. We can store data in this type but only once. In this type we use a dye layer and a laser beam with specific intensity is used to write on that layer.
        - The third type is rewriteable CD.
            
            ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2031.png)
            
            ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2032.png)
            
- DVD
    - Stands for Digital Video/Versatile Disk.
    - Has larger capacity to store data.
    - The laser beam radius is reduced, hence the track thickness is minimized which results in adding more area to the track.
        
        ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2033.png)
        
- DVD vs CD
    - Since track thickness is reduced, the space between loops and the distance between pits are reduced.
    - You may use two surface to increase the storage space. You can access each surface with different laser beam intensities.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2034.png)
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2035.png)
    
- Magnetic tape - FYI.
    
    ![Untitled](CH6%20-%20External%20Memory%20c63eafd391594d92ba596f3edb84c4b6/Untitled%2036.png)