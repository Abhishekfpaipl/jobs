<template>
    <div>
        <div class="query border rounded-circle" style="background-color: var(--brand-color)" @click="openModal">
            <img src="/img/logo.svg" style="width: 40px; height: 40px;" alt="">
        </div>

        <div class="modal" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
            aria-hidden="true" :class="{ 'show': showModal }">
            <div class="modal-dialog modal-dialog-centered modal-lg " role="document">
                <div class="modal-content text-white position-relative">
                    <div class="modal-body p-0">
                        <div class="container text-dark bg-white my-3">
                            <div class="row rounded  border mx-1 p-3 text-bg-dark align-items-center">
                                <div class="col-md-3">
                                    <img src="/img/users/1.png" alt="" class="rounded-circle"
                                        style="width: 120px; height: 120px;">
                                </div>
                                <div class="col-md-9 text-center text-md-start">
                                    <p class="my-1 fs-2 fw-bold">Mariana Anderson</p>
                                    <p class="d-inline-block text-start my-1 fs-5">Marketing Manager</p>
                                    <div class="d-flex gap-2 my-1 fs-5">
                                        <span>Fameset</span>
                                        <div class="">
                                            <span v-for="(star, index) in stars" :key="index" class="text-warning">
                                                <i v-if="star === 'full'" class="bi bi-star-fill"></i>
                                                <i v-else-if="star === 'half'" class="bi bi-star-half"></i>
                                                <i v-else class="bi bi-star"></i>
                                            </span>
                                        </div>
                                        <span>{{ resume.stars }} Rating</span>
                                        <!-- <i class="bi bi-star-fill text-warning ms-2"></i> -->
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="container text-dark bg-white mt-4">
                            <div class="row row-cols-4 row-cols-md-4 mx-1 g-1">
                                <div v-for="(item, index) in fav" :key="index" class="col">
                                    <div class="p-2 card shadow"
                                        style="background-color: #FFF5DD !important;border-color: #FFCE56 !important;">
                                        <div class="d-md-flex justify-content-between align-items-center border-bottom pb-2"
                                            style="border-color: #FFCE56 !important;">
                                            <i :class="item.iconClass" class="text-dark fs-5"></i>
                                            <p class="fw-bold smaller mb-0">{{ item.label }}</p>
                                        </div>
                                        <p class="fw-bold fs-1 mb-0 d-flex justify-content-center align-items-center">
                                            <AutoCounter :data="item.data" />&nbsp;+
                                        </p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="mx-3 pb-3 pt-4">
                            <button class="w-100 btn btn-warning fs-4"><span class="text-capitalize">We'd Love To Have Your Feedback</span> <i class="bi bi-arrow-right "></i></button>
                        </div>
                    </div>
                    <div class="position-absolute rounded-circle wh-40 bg-warning text-dark px-2 p-1"
                        @click="closeModal" style="top: -1%;right: -1%;">
                        <i class="bi bi-x fs-5"></i>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import AutoCounter from "@/components/AutoCounter.vue"
export default {
    props: {
        resume: {
            type: Object,
            required: true
        }
    },
    components: {
        AutoCounter
    },
    data() {
        return {
            showModal: false,
            fav: [
                {
                    iconClass: 'bi bi-trophy-fill',
                    iconColor: '#BCDFFB',
                    data: 10,
                    label: 'Awards',

                },
                {
                    iconClass: 'bi bi-award-fill',
                    iconColor: '#C9E7CA',
                    data: 10,
                    label: 'Rewards'
                },
                {
                    iconClass: 'bi bi-shield-fill-check',
                    iconColor: '#FFB2B2',
                    data: 50,
                    label: 'Badges'
                },
                {
                    iconClass: 'bi bi-hand-thumbs-up-fill',
                    iconColor: '#BCDFFB',
                    data: 10,
                    label: 'Likes',

                },
                {
                    iconClass: 'bi bi-megaphone-fill',
                    iconColor: '#FFB2B2',
                    data: 50,
                    label: 'Promoters'
                },
                {
                    iconClass: 'bi bi-heart-fill',
                    iconColor: '#C9E7CA',
                    data: 10,
                    label: 'Thankful'
                },
                {
                    iconClass: 'bi bi-chat-dots-fill',
                    iconColor: '#C9E7CA',
                    data: 10,
                    label: 'Reviews'
                },
                {
                    iconClass: 'bi bi-people-fill',
                    iconColor: '#C9E7CA',
                    data: 10,
                    label: 'Users'
                },
            ],
            rating: 4.5,
        };
    },
    mounted() {
        if (!localStorage.getItem('popupShown')) {
            setTimeout(() => {
                this.showModal = true;
            }, 2000);
        }
    },
    methods: {
        openModal() {
            this.showModal = true;
        },
        closeModal() {
            this.showModal = false;
            localStorage.setItem('popupShown', 'true');
        },
    },
    computed: {
        stars() {
            const fullStars = Math.floor(this.rating);
            const halfStar = this.rating % 1 !== 0;
            return Array.from({ length: 5 }, (_, index) => {
                if (index < fullStars) {
                    return 'full';
                } else if (index === fullStars && halfStar) {
                    return 'half';
                } else {
                    return 'empty';
                }
            });
        }
    }
};
</script>

<style scoped>
/* Optional: Add custom styles for the modal */
.modal {
    display: none;
    background: rgba(0, 0, 0, 0.5);
    /* semi-transparent background */
    transition: opacity 0.3s ease;
}

.modal.show {
    display: block;
    opacity: 1;
}

.query {
    z-index: 9;
    position: fixed;
    bottom: 10%;
    right: 10px;
    padding: 5px;
    cursor: pointer;
    border-radius: 5px;
    display: flex;
    align-items: center;
}
</style>
