<template>
  
    <div class="sticky-nav my-4">
        <div class="d-flex gap-3 p-3 ps-md-5 overflow-x-scroll py-3" id="scroll"
            style="background-color:rgba(255, 206, 86, 0.2); border:1px solid rgba(255, 206, 86, 1) !important;">
            <div v-for="(section, index) in sections" :key="index">
                <a :href="'#' + section.id" class="nav-link text-dark" @click.prevent="scrollToSection(section.id)"
                    :class="{ active: activeSection === section.id }">
                    {{ section.name }}
                </a>
            </div>
        </div>
    </div>

    <div class="container">
        <section v-for="(section, index) in sections" :key="index" :id="section.id" class="section"
            style="padding-top:30px">
            <h3 class="text-center bill"><span class="fs-2">~ {{ section.name }} ~</span></h3>
            <!-- <h3 class="p-2 text-center my-4 cutout">
                <span></span>
            </h3> -->
            <component :is="section.component"></component>
        </section>
    </div>

</template>

<script>
import ContactSection from '@/components/ContactSection.vue';
import AboutusSection from "@/components/AboutusSection.vue";
import BusinessSection from "@/components/BusinessSection.vue";
import GalleryCollage from "@/components/GalleryCollage.vue";
export default {
    name: "InformationSection",
    components: {
        ContactSection,
        AboutusSection,
        BusinessSection,
        GalleryCollage,
    },
    data() {
        return {
            rating: 0,
            reviewText: "",
            sections: [
                { id: 'Collection', name: 'Collection', component: 'BusinessSection' },
                { id: 'Timeline', name: 'Timeline', component: 'ContactSection' },
                { id: 'Gallery', name: 'Gallery', component: 'GalleryCollage' },
                { id: 'About', name: 'About', component: 'AboutusSection' },
                { id: 'Connect', name: 'Connect', component: 'ContactSection' },
                // { id: 'Contact', name: 'Contact', component: 'ContactSection' }, 
                // { id: 'Social', name: 'Social', component: 'ContactSection' }, 
            ],
            activeSection: '',
        }
    },
    mounted() {
        window.addEventListener('scroll', this.handleScroll);
    },
    unmounted() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        isActive(id) {
            return this.$route.hash === "#" + id;
        },
        scrollToSection(id) {
            const el = document.getElementById(id);
            if (el) {
                el.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }
        },
        handleScroll() {
            const scrollPosition = window.scrollY;
            this.sections.forEach(section => {
                const el = document.getElementById(section.id);
                if (el && scrollPosition >= el.offsetTop - 200) {
                    this.activeSection = section.id;
                }
            });
            // Change navbar background color conditionally
            this.navbarDark = scrollPosition > 50; // Example threshold for changing navbar background
        },
        setRating(star) {
            this.rating = star;
        },
    }
}
</script>
<style scoped>
.nav-link.active {
    background-color: transparent;
    color: black !important;
    border-bottom: 2px solid black;
}

.sticky-nav {
    /* position: -webkit-sticky; */
    /* For Safari */
    position: sticky;
    top: 0 !important;
    z-index: 1000;
    background-color: white;
}
</style>