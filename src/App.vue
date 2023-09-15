<template>
  <h1 class="kkk">Booking of coffee</h1>
  <br>
  <div>
    <div class="container text-center ">
      <div class="row align-items-start ">
        <div class="col " v-for="(destination, index) in travelList" :key="index">
          <div class="card m-3 " style="width: 20rem;">
            <img :src="destination.img" class="card-img-top fixed-image-height" alt="...">
            <div class="card-body  ">
              <h5 class="card-title">{{ destination.name }}</h5>
              <p class="card-text">{{ destination.decipe }}</p>
              <p class="card-text">{{ destination.timeOpen }}</p>
              <p class="card-text">{{ destination.dayClose }}</p>
              <div class="form-floating mb-1">
              <input class="form-control" type="number" v-model="destination.numBookings" placeholder="Number of Bookings">
              <label for="floatingInputValue">จำนวนโต๊ะ</label></div>
              <div class="form-floating mb-1">
              <input class="form-control" type="text" v-model="destination.bookerName" placeholder="Booker's Name">
              <label for="floatingInputValue">ชื่อผู้จอง</label></div>
              <div class="form-floating mb-1">
              <input class="form-control" type="date" v-model="destination.bookingDate" placeholder="Booking Date">
              <label for="floatingInputValue">วันที่</label></div>
              <div class="form-floating mb-1">
              <input class="form-control" type="text" v-model="destination.phoneNumber" placeholder="Phone Number">
              <label for="floatingInputValue">เบอร์โทร</label></div>
              <div class="form-floating mb-1">
              <input class="form-control" type="time" v-model="destination.bookingTime" placeholder="Booking Time">
              <label for="floatingInputValue">เวลา</label></div>

              <a class="btn" @click="booking(destination)">จองร้าน</a>
            
          </div>
        </div>
      </div>
    </div>
  </div>
    <h1 class="lisss">รายการจอง</h1>
    <table class="table table-pink table-striped" v-if="bookinglist.length > 0"> 
      <thead>
        <tr>
          <th scope="col">ลำดับ</th>
          <th scope="col">ชื่อร้าน</th>
          <th scope="col">จำนวนโต๊ะ</th>
          <th scope="col">ชื่อผู้จอง</th>
          <th scope="col">วันที่จอง</th>
          <th scope="col">เบอร์โทร</th>
          <th scope="col">เวลาจอง</th>
        </tr>
      </thead>
      <tbody class="table-group-divider">
        <tr v-for="(booking, index) in bookinglist" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ booking.name }}</td>
          <td>{{ booking.numBookings }}</td>
          <td>{{ booking.bookerName }}</td>
          <td>{{ booking.bookingDate }}</td>
          <td>{{ booking.phoneNumber }}</td>
          <td>{{ booking.bookingTime }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const travelList = ref([
{name: 'Treespresso cafe',
price: 80,
size: { s: 80, m: 150, l: 200 },
img: 'https://www.ryoiireview.com/upload/article/202304/1681731156_d018557a4a10aed6c8f450ad0db6d60d.jpg',
decipe : 'คาเฟ่ย่านสถานีรถไฟค่ะ ร้านนี้บรรยากาศดีมากก อยู่ใต้ต้นร่มใหญ่มีความร่มรื่น เขียวขจี ตัวร้านจะมีเน้นโทนไม้ ให้ความรู้สึกอบอุ่น มีความผ่อนคลาย จะมานั่งพักผ่อนชิลๆ ก็เหมาะ หรือจะมาถ่ายก็ดีงามสุดๆ! ในส่วนของเมนูทางร้านก็จัดเต็มค่ะ มีครบทั้งอาหารจานหลัก ของหวาน และเครื่องดื่มเช่น orange tea, ชุดอาหารเช้า, ฮันนี่โทสต์ ',
timeOpen : 'เปิดบริการ : 08.30-18.00 น.',
dayClose :'เปิดทุกวัน'},
{name:'Polaris Sunrise Café',
price:120,
size:{s:80,m:150,l:200},
img:"https://www.ryoiireview.com/upload/article/202304/1681733919_1dc9da5619cecf386917f0533fd4ce31.jpg",
decipe : 'บรรยากาศดีสไตล์มินิมอล แถมรายล้อมด้วยต้นไม้เขียวขจี บรรยากาศดีมากก ที่นั่งมีทั้งโซน indoor และ outdoor จะมุมไหนก็น่านั่งค่ะ ทั้งต้นไม้ น้ำตก และลำธาร แถมทางร้านยังมีปลั๊กพร้อมให้บริการสำหรับคนมองหาที่ทำงานด้วยนะ! สำหรับเมนูของทางร้านก็ครบครัน ทั้งอาหารจานเดียว อาหารเช้า ของทานเล่น เบเกอรี และเครื่องดื่มมากมาย',
timeOpen : 'เปิดบริการ : 07.30-17.00 น.',
dayClose :'เปิดทุกวัน'},
{name:'MOJI Pool.Villa.icecream ',
price:150,
size:{s:120,m:180,l:250},
img:"https://www.ryoiireview.com/upload/article/202304/1681732797_e6ba6dfb2985ae2d0acbfe4e02e938b4.jpg",
decipe : 'คาเฟ่สุดคิวววท์ที่เพิ่งเปิดใหม่ ร้านนี้ตกแต่งออกมาได้น่ารักมากก โดยจะตกแต่งออกมาในสไตล์ญี่ปุ่น เหมือนยกญี่ปุ่นมาไว้ที่เชียงใหม่ บอกเลยว่ามีมุมให้ถ่ายรูปเพียบ! ในส่วนของเมนูก็เอาใจคนรักของหวาน มีทั้งเครื่องดื่มสตล์ญี่ปุ่น, ไอศกรีมโฮมเมดสไตล์ญี่ปุ่น รสอร่อยแบบสุดครีเอทจากวัตถุดิบธรรมชาติ 100%, โมจิปั้นสดไส้สตรอว์เบอร์ และเลม่อนเค้ก',
timeOpen : 'เปิดบริการ : 11.00-18.00 น.',
dayClose :'ปิดวันจันทร์'},
{name:'Kramfeine',
price:100,
size:{s:120,m:160,l:220},
img:"https://www.ryoiireview.com/upload/article/202304/1681715844_d21d365be6d7d62ca60369c9659a60f2.jpg",
decipe : 'คาเฟ่ที่มาในบรรยากาศสบายๆ และมีเมนูเอาใจคนรักกาแฟสุดๆ เพราะทางร้านจะมีเมล็ดกาแฟให้ลูกค้าสามารถเลือกได้ตามความชอบทั้งเมล็ดกาแฟแบบคั่วอ่อน คั่วกลาง และคั่วเข้มค่ะ แต่ที่นี่ไม่ได้มีดีแค่กาแฟเท่านั้น! ยังมีเมนูอาหาร และเบเกอรีที่เป็นสูตรของทางร้านเองสไตล์โฮมเมดอีกด้วยค่ะ',
timeOpen : 'เปิดบริการ : 08.30-16.30 น.',
dayClose :'ปิดวันอังคาร'},
{name:'Millilit Cafe',
price:90,
size:{s:110,m:150,l:210},
img:"https://www.ryoiireview.com/upload/article/202304/1681716120_0eb16eb4a1bf3b689ed1a5f3431b2912.jpg",
decipe : 'คาเฟ่ที่มาในบรรยากาศเก๋สุดๆ แต่จะเปลี่ยนธีมร้านไปเรื่อยๆ อีกด้วยล่ะค่ะ สำหรับร้านนี้ถือว่าเป็นคาเฟ่ที่เอาใจสายหวานอย่างเมนูโกโก้โคตรเข้มข้น ที่จะมีให้เลือกคนข้นถึงสามระดับด้วยกัน ทั้ง Dark Medium และ Light ค่ะ บอกเลยว่ามาร้านนี้แล้วต้องมาและนอกจากนี้ก็ยังมีเมนูอื่นๆอีกมากมาย',
timeOpen : 'เปิดบริการ : 07.30-18.00 น.',
dayClose :'เปิดทุกวัน'},
{name:'Soul Café mju',
price:90,
size:{s:110,m:150,l:210},
img:"https://www.ryoiireview.com/upload/article/202207/1658477803_032b2cc936860b03048302d991c3498f.jpg",
decipe : 'คาเฟ่บรรยากาศน่านั่งอีกหนึ่งร้านที่มีเมนูเบเกอรีสไตล์ Homemade ราคาสบายกระเป๋า รสชาติดีเกินราคา ในย้านแม่โจ้นักศึกษาแม่โจ้ห้ามพลาด มีเมนูให้เลือกทานมากมายเลย นอกจากนี้ก็ยังมีเมนูเครื่องดื่มอีกด้วย และถ้าใครที่เป็นสายกาแฟ บอกเลยว่าร้านนี้ไม่ควรพลาด',
timeOpen : 'เปิดบริการ : 08.00-18.00 น.',
dayClose :'เปิดทุกวัน'},
]);





const bookinglist = ref([]);

const booking = (destination) => {
  if (destination.numBookings > 0) {
    bookinglist.value.push({
      name: destination.name,
      decipetion : destination.decipe,
      dayOff:destination.dayClose,
      timeStart:destination.timeOpen,
      numBookings: destination.numBookings,
      bookerName: destination.bookerName,
      bookingDate: destination.bookingDate,
      phoneNumber: destination.phoneNumber,
      bookingTime: destination.bookingTime,
    });
  }
};
</script>

<style>
.fixed-image-height {
  height: 250px; /* Set your desired fixed height for the images */
  object-fit: cover; /* Preserve the aspect ratio */
}
.card{
background-color: #ffbcec;
}

</style>
