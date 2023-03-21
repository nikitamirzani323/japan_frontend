<script>
    import { initializeApp } from "firebase/app";
    import { getDatabase, ref, onValue } from "firebase/database";
    import dayjs from "dayjs";
    import Carousel from '../lib/Carousel.svelte'

    const firebaseConfig = {
        apiKey: "AIzaSyBqVRbGvJBb1JEfKYyN6jgocZjzsx2lN2A",
        authDomain: "dazzling-pillar-328210.firebaseapp.com",
        databaseURL: "https://dazzling-pillar-328210-default-rtdb.asia-southeast1.firebasedatabase.app",
        projectId: "dazzling-pillar-328210",
        storageBucket: "dazzling-pillar-328210.appspot.com",
        messagingSenderId: "770359422621",
        appId: "1:770359422621:web:7933922e00547dc735ee74"
    };
    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);
    const japanday = ref(db, "japanday");
    const japannight = ref(db, "japannight");
    
    let lang = localStorage.getItem("lang");
    let livedraw_text_1 = "";
    let livedraw_text_2 = "";
    let livedraw_text_3 = "";
    let livedraw_text_4 = "";
    let livedraw_text_5 = "";
    let livedraw_text_6 = false;
    if(lang == null || lang == "english"){
        livedraw_text_1 = "WINNING NUMBER";
        livedraw_text_2 = "6D RESULT";
        livedraw_text_3 = "DRAW";
        livedraw_text_4 = "DATE";
        livedraw_text_5 = "We accept these payment method";
        livedraw_text_6 = true;
    }else{
        livedraw_text_1 = "SỐ TRÚNG THƯỞNG";
        livedraw_text_2 = "KẾT QUẢ 6D";
        livedraw_text_3 = "VẼ TRANH";
        livedraw_text_4 = "NGÀY";
        livedraw_text_5 = "Chúng tôi chấp nhận các phương thức thanh toán này";
        livedraw_text_6 = false;
    }
    
  
    let date_draw = "";
    let prize1 = "";
    let prize2 = "";
    let prize3 = "";
    let date_draw_night = "";
    let prize1_night = "";
    let prize2_night = "";
    let prize3_night = "";
   

    let day_img_1_prize1 = "images/ball-null.png";
    let day_img_2_prize1 = "images/ball-null.png";
    let day_img_3_prize1 = "images/ball-null.png";
    let day_img_4_prize1 = "images/ball-null.png";
    let day_img_1_prize2 = "images/ball-null.png";
    let day_img_2_prize2 = "images/ball-null.png";
    let day_img_3_prize2 = "images/ball-null.png";
    let day_img_4_prize2 = "images/ball-null.png";
    let day_img_1_prize3 = "images/ball-null.png";
    let day_img_2_prize3 = "images/ball-null.png";
    let day_img_3_prize3 = "images/ball-null.png";
    let day_img_4_prize3 = "images/ball-null.png";

    let night_img_1_prize1 = "images/ball-null.png";
    let night_img_2_prize1 = "images/ball-null.png";
    let night_img_3_prize1 = "images/ball-null.png";
    let night_img_4_prize1 = "images/ball-null.png";
    let night_img_1_prize2 = "images/ball-null.png";
    let night_img_2_prize2 = "images/ball-null.png";
    let night_img_3_prize2 = "images/ball-null.png";
    let night_img_4_prize2 = "images/ball-null.png";
    let night_img_1_prize3 = "images/ball-null.png";
    let night_img_2_prize3 = "images/ball-null.png";
    let night_img_3_prize3 = "images/ball-null.png";
    let night_img_4_prize3 = "images/ball-null.png";
   
    onValue(japanday, (snapshot) => {
        const data = snapshot.val();
        date_draw = dayjs(data["datedraw"]).format("MMMM DD, YYYY");;
        prize1 = data["prize1"];
        prize2 = data["prize2"];
        prize3 = data["prize3"];
        
        
        if(prize1 != ""){
            day_img_1_prize1 = getImage(prize1[0])
            day_img_2_prize1 = getImage(prize1[1])
            day_img_3_prize1 = getImage(prize1[2])
            day_img_4_prize1 = getImage(prize1[3])
        }
        if(prize2 != ""){
            day_img_1_prize2 = getImage(prize2[0])
            day_img_2_prize2 = getImage(prize2[1])
            day_img_3_prize2 = getImage(prize2[2])
            day_img_4_prize2 = getImage(prize2[3])
        }
        if(prize3 != ""){
            day_img_1_prize3 = getImage(prize3[0])
            day_img_2_prize3 = getImage(prize3[1])
            day_img_3_prize3 = getImage(prize3[2])
            day_img_4_prize3 = getImage(prize3[3])
        }
        
        
    });
    onValue(japannight, (snapshot) => {
        const data = snapshot.val();
        date_draw_night = dayjs(data["datedraw"]).format("MMMM DD, YYYY");;
        prize1_night = data["prize1"];
        prize2_night = data["prize2"];
        prize3_night = data["prize3"];
        
        
        if(prize1_night != ""){
            night_img_1_prize1 = getImage(prize1_night[0])
            night_img_2_prize1 = getImage(prize1_night[1])
            night_img_3_prize1 = getImage(prize1_night[2])
            night_img_4_prize1 = getImage(prize1_night[3])
        }
        if(prize2_night != ""){
            night_img_1_prize2 = getImage(prize2_night[0])
            night_img_2_prize2 = getImage(prize2_night[1])
            night_img_3_prize2 = getImage(prize2_night[2])
            night_img_4_prize2 = getImage(prize2_night[3])
        }
        if(prize3_night != ""){
            night_img_1_prize3 = getImage(prize3_night[0])
            night_img_2_prize3 = getImage(prize3_night[1])
            night_img_3_prize3 = getImage(prize3_night[2])
            night_img_4_prize3 = getImage(prize3_night[3])
        }
        
        
    });
    
   
    function getImage(e,tipe) {
        let urlimg = "";
        switch (e) {
            case "0":
                urlimg = "images/ball-0.png";
                break;
            case "1":
                urlimg = "images/ball-1.png";
                break;
            case "2":
                urlimg = "images/ball-2.png";
                break;
            case "3":
                urlimg = "images/ball-3.png";
                break;
            case "4":
                urlimg = "images/ball-4.png";
                break;
            case "5":
                urlimg = "images/ball-5.png";
                break;
            case "6":
                urlimg = "images/ball-6.png";
                break;
            case "7":
                urlimg = "images/ball-7.png";
                break;
            case "8":
                urlimg = "images/ball-8.png";
                break;
            case "9":
                urlimg = "images/ball-9.png";
                break;
        }
        return urlimg;
    }
    let listvietnam = [
        {tgl:"2023-03-01",prize_1:"1134",prize_2:"1532",prize_3:"0923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2134",prize_2:"2532",prize_3:"1923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"3134",prize_2:"3532",prize_3:"2923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"4134",prize_2:"4532",prize_3:"3923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"5134",prize_2:"5532",prize_3:"4923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"6134",prize_2:"6532",prize_3:"5923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"7134",prize_2:"7532",prize_3:"6923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"8134",prize_2:"8532",prize_3:"7923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"9134",prize_2:"9532",prize_3:"8923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"0134",prize_2:"0532",prize_3:"9923",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2234",prize_2:"1632",prize_3:"0023",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2334",prize_2:"1732",prize_3:"0123",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2434",prize_2:"1832",prize_3:"0223",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2534",prize_2:"1932",prize_3:"0323",prize_4:"2123"},
        {tgl:"2023-03-01",prize_1:"2634",prize_2:"1032",prize_3:"0423",prize_4:"2123"},
    ];
   
  </script>
<section class="hidden lg:flex">
    <Carousel />
</section>
<section class="lg:flex w-full gap-1 bg-[#ffda92] p-2 lg:p-10">
    <center>
        <img class="w-5/6" src="images/imgwinning.png" alt="">
        <img class="w-1/2" src="images/imgwinningjapan.png" alt="">
        <span class="text-[#4fb47d]">Thurday , 16 Maret 2023</span>
        <section class="lg:flex w-full lg:w-4/5 rounded-xl   bg-[#fff1d6] border-4 border-[#00989f] p-2 lg:p-5 ">
            <div class="flex flex-col lg:flex lg:flex-row w-full gap-1 ">
                <div class="card w-full lg:w-4/5  rounded-xl lg:p-2 lg:m-5 border-4 border-[#00989f] bg-[#ffda92]">
                    <div class="card-body p-1 mb-1 ">
                        <center class="p-2 font-bold w-full">
                            <img src="images/shizoukaday4x.png" alt="">
                        </center>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl  lg:text-2xl font-bold self-center text-[#4fb47d]">
                                Prize 1st 賞品1位
                            </div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{day_img_1_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_2_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_3_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_4_prize1}" alt="">
                            </div>
                        </div>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl lg:text-2xl font-bold self-center text-[#4fb47d]">Prize 2nd 2等賞</div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{day_img_1_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_2_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_3_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_4_prize2}" alt="">
                            </div>
                        </div>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl lg:text-2xl font-bold self-center text-[#4fb47d]">Prize 3rd 3等賞</div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{day_img_1_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_2_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_3_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{day_img_4_prize3}" alt="">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="card w-full lg:w-4/5 rounded-xl lg:p-2 lg:m-5 border-4 border-[#00989f] bg-[#ffda92]">
                    <div class="card-body p-1 mb-1 ">
                        <center class="p-2 font-bold w-full">
                            <img src="images/shizoukanight4x.png" alt="">
                        </center>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl lg:text-2xl font-bold self-center text-[#4fb47d]">Prize 1st 賞品1位</div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{night_img_1_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_2_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_3_prize1}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_4_prize1}" alt="">
                            </div>
                        </div>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl lg:text-2xl font-bold self-center text-[#4fb47d]">Prize 2nd 2等賞</div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{night_img_1_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_2_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_3_prize2}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_4_prize2}" alt="">
                            </div>
                        </div>
                        <div class="lg:flex flex-col justify-center gap-1">
                            <div class="w-full text-center text-xl lg:text-2xl font-bold self-center text-[#4fb47d]">Prize 3rd 3等賞</div>
                            <div class="flex justify-center gap-1 w-full ">
                                <img class="w-14 lg:w-[80px]" src="{night_img_1_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_2_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_3_prize3}" alt="">
                                <img class="w-14 lg:w-[80px]" src="{night_img_4_prize3}" alt="">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
        </section>
    </center>
   
</section>

<section class="mt-0 bg-black">
    <center class="pt-10">
        <span class="text-[#00989f] text-xl lg:text-4xl ">
            政府が管理する信頼できるウェブサイト
        </span>
        <img class="w-5/6 lg:w-4/5 mt-5" src="images/supportbank_2.png" alt="">
    </center>
    <div class="flex w-full justify-center items-stretch mt-5">
        <div class="flex gap-5 mt-2 self-center">
            <img class="w-[20px] lg:w-[40px]" src="images/visa.png" alt="">
            <img class="w-[20px] lg:w-[40px]" src="images/master.png" alt="">
            <img class="w-[20px] lg:w-[40px]" src="images/maestro.png" alt="">
            <img class="w-[20px] lg:w-[40px]" src="images/e_pro.png" alt="">
            <img class="w-[20px] lg:w-[40px]" src="images/age.png" alt="">
            <img class="w-[20px] lg:w-[40px]" src="images/curacao.png" alt="">
        </div>
    </div>
    <center class="mt-10 lg:mt-20 pb-10">
        <span class="text-[#00989f] text-lg">
            Copyright © 2020 - 静岡市 宝くじ
        </span>
    </center>
</section>