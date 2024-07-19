<template>
  <div class=" ">
    <DigitalCardNav />
    <ProfileSection :user="user"/> 
    <InfoSection />
    <InformationSection />
  </div>
</template>

<script>
 
import ProfileSection from '@/components/ProfileSection.vue'
import DigitalCardNav from '@/components/DigitalCardNav.vue'
import InfoSection from '@/components/digitalcard/InfoSection.vue';
import InformationSection from '@/components/InformationSection.vue';

export default {
  name: "DigitalCard",
  components: {
    ProfileSection,
    DigitalCardNav, 
    InfoSection,
    InformationSection,
  },
  data() {
    return {
      user: {
        image:"/img/users/1.png",
        name: "John Doe",
        post: "Marketing Manager",
        discription: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Impedit inventore nisi odio consectetur laudantium reiciendis dolor sit porro eligendi! Doloremque."
      }
    }
  },

};
</script>