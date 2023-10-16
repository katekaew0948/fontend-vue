<template>
  <v-container class="fill-height" fluid>
    <v-fade-transition mode="out-in">
      <v-row>
        <v-col>
          <v-card>
            <v-carousel>
              <v-carousel-item
                v-for="(item, i) in items"
                :key="i"
                :src="item.src"
                reverse-transition="fade-transition"
                transition="fade-transition"
                class="grey darken-4"
              ></v-carousel-item>
            </v-carousel>
            <v-card-title class="headline">
              {{artists.penName}} รับวาดภาพประกอบฉาก
            </v-card-title>
            <v-card-text>
              <div class="red--text">Rate Price : {{artists.ratePrice}}</div>

              <div class="my-4 text-subtitle-1">Pen Name : {{artists.penName}}</div>
              <div>
                Contact : <br />
                LineId : {{artists.contact}} <br />
                Tel : {{artists.contact}}  <br />
              </div>
            </v-card-text>
            <v-divider class="mx-4"></v-divider>

            <v-card-title>Detail</v-card-title>
            <v-card-text>
              <v-row align="center" class="mx-0">
                <div class="my-4 text-subtitle-1">
                  {{artists.detail}}
                  
                  / PSD/ TIFF ระบุได้เลยค่ะว่าต้องการเป็น RGB/ CMYK
                  ขนาดของภาพไม่เกิน 9,000 * 9,000 pixels หรือ 30 * 30 นิ้ว
                  ความละเอียดสูงสุด 300 dpi <br /><br />

                  สำหรับ mood & tone หากลูกค้ามีรูปแบบงานที่สนใจอยู่
                  สามารถส่งให้ดูก่อนได้ค่ะ
                  เนื่องด้วยเนื้องานมีความยากง่ายและลายละเอียดต่างกัน
                  ราคาจึงมีความแตกต่างกันนะคะ
                </div>
                <div class="my-4 font-weight-bold">
                  ขั้นตอนการทำงาน <br />
                  1. บรีฟลักษณะงานที่ต้องการและวัตถุประสงค์ที่จะนำไปใช้
                  หากมีรูปแบบหรือตัวอย่างที่สนใจเป็นพิเศษจะช่วยในการออกแบบให้ตรงใจผู้ว่าจ้างได้มากยิ่งขึ้น <br />
                  2. ประเมินราคา พร้อมแจ้งระยะเวลาของการทำงาน <br />
                </div>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-fade-transition>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        src: "https://cdn.pixabay.com/photo/2012/03/01/00/21/bridge-19513_1280.jpg",
      },
      {
        src: "https://cdn.pixabay.com/photo/2022/11/15/12/23/winter-7593872_1280.jpg",
      },
      {
        src: "https://cdn.pixabay.com/photo/2021/10/27/13/15/digital-graphicscat-6747298_1280.jpg",
      },
      {
        src: "https://cdn.pixabay.com/photo/2023/08/09/08/17/mouse-8178945_1280.jpg",
      },
    ],
    artists: [],
    artistId: 1,

  }),

  created () {
      this.getArtist()
    },

  methods: {
    async getArtist(){
        try {
            var data = await this.axios.get('http://localhost:9000/artist/'+ this.artistId)
            if(data.status == 200){
                console.log('data artist ===> ' ,data)
                this.artists = data.data
            }
        } catch (error) {
            
        }
    }
  }
};
</script>

<style>
 .fill-height{
     background-image: url('../assets/starry_sky.jpg');
    background-repeat: no-repeat;
    background-size: cover;
 }
</style>