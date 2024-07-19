<template>
    <div class="container">
        <div class="row">
            <div class="col-md-3 p-4 pb-0">
                <div class="mt-4">
                    <img :src="resume.photo" alt="Profile Photo" class="rounded-circle img-fluid mb-3"
                        style="max-width: 150px;">
                </div>
            </div>
            <div class="col-md-9 p-4 pb-0">
                <div class="mt-4 text-md-start text-center border-bottom border-dark border-2">
                    <h1>{{ resume.name }}</h1>
                    <h5>{{ resume.position }}</h5>
                    <p>{{ resume.description }}</p>
                </div>
            </div>
        </div>
        <div class="row">
            <!-- Left column -->
            <div class="col-md-3 text-dark p-4 text-start">
                <h3 class="mt-4 border-bottom">Ratings</h3>
                <div class="d-flex justify-content-between align-items-center py-2 border-bottom"
                    v-for="(rating, index) in resume.rating" :key="index">
                    <p class="mb-0">{{ rating.name }}</p>
                    <ReviewRating :rating="rating.stars" />
                </div>

                <h3 class="mt-4 border-bottom">Contact</h3>
                <p><i class="bi bi-telephone"></i>&nbsp;: <span>{{ resume.phone }}</span></p>
                <p><i class="bi bi-envelope"></i>&nbsp;: <span>{{ resume.email }}</span></p>
                <p><i class="bi bi-geo-alt"></i>&nbsp;: <span>{{ resume.address }}</span></p>

                <h3 class="mt-4 border-bottom">Technical Skills</h3>
                <div class="" v-for="(skill, index) in resume.skills" :key="index">
                    <p class="mb-1 mt-3 text-uppercase">{{ skill.skill }} </p>
                    <div class="progress rounded-0" role="progressbar" aria-label="Danger example" aria-valuenow="100"
                        aria-valuemin="0" aria-valuemax="100">
                        <div class="progress-bar bg-danger" :style="{ width: skill.percent + '%' }"> {{ skill.percent }}
                            %</div>
                    </div>
                </div>
                <h3 class="mt-4 border-bottom">Expertise</h3>
                <ul>
                    <li v-for="skill in resume.expertise" :key="skill">{{ skill }}</li>
                </ul>

                <h3 class="mt-4 border-bottom">Language</h3>
                <ul>
                    <li v-for="lang in resume.languages" :key="lang">{{ lang }}</li>
                </ul>
            </div>

            <!-- Right column -->
            <div class="col-md-9 p-4 text-start">
                <h3 class="mt-4 border-bottom">Experience</h3>
                <div class="timeline position-relative mx-auto">
                    <div class="timeline-item pe-md-5 pe-0" v-for="(job, index) in resume.experience" :key="index">
                        <div class="position-relative shadow bg-rounded bg-white">
                            <div class="d-md-flex gap-3 text-bg-dark p-3">
                                <img :src="img" class="rounded" alt="" style="width: 50px; height: 50px;">
                                <h5 class="mb-0">{{ job.company }}</h5>
                            </div>
                            <div class="text-bg-secondary text-center p-2">
                                <p class="mb-0">{{ job.period }}</p>
                            </div>
                            <div class="p-3">
                                <p class="">{{ job.position }}</p>
                                <p class="timeline-description">{{ job.description }}</p>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- <div class="order-stepper">
                    <div v-for="(job, index) in resume.experience" :key="index" class="mb-4 active" id="step">
                        <h5>{{ job.period }}</h5>
                        <p><strong>{{ job.company }}</strong></p>
                        <p>{{ job.position }}</p>
                        <p>{{ job.description }}</p>
                    </div>
                </div> -->
                <h3 class="mt-4 border-bottom">Education</h3>
                <div class="row m-2" v-for="(edu, index) in resume.education" :key="index">
                    <div class="text-center col-12 fw-bold">{{ edu.year }}</div>
                    <div class="border col-6 bg-light py-3">{{ edu.degree }}</div>
                    <div class="border col-6 py-3 bg-white">{{ edu.school }}</div>
                </div>
                <h3 class="mt-4 border-bottom">Certificates</h3>
                <div class="row m-2" v-for="(edu, index) in resume.certificates" :key="index">
                    <div class="text-center col-12 fw-bold">{{ edu.year }}</div>
                    <div class="border col-6 bg-light py-3">{{ edu.degree }}</div>
                    <div class="border col-6 py-3 bg-white">{{ edu.school }}</div>
                </div>
                <h3 class="mt-5 border-bottom">Contact</h3>
                <ContactSection />
                <h3 class="mt-5 border-bottom">Reference</h3>
                <div class="row">
                    <div v-for="ref in resume.references" :key="ref.name" class="col-md-6">
                        <p><strong>{{ ref.name }}</strong></p>
                        <p>{{ ref.position }}, {{ ref.company }}</p>
                        <p><i class="bi bi-telephone"></i>&nbsp;: <span>{{ ref.phone }}</span></p>
                        <p><i class="bi bi-envelope"></i>&nbsp;: <span>{{ ref.email }}</span></p>
                    </div>
                </div>
            </div>
        </div>

    </div>
    
    <WelcomeModal :resume="resume"/>
</template>

<script>
import ContactSection from "@/components/ContactSection.vue";
import ReviewRating from "@/components/ReviewRating.vue";
import WelcomeModal from '@/components/WelcomeModal.vue';
export default {
    name: 'ResumeComponent',
    components: {
        ContactSection,
        ReviewRating,
        WelcomeModal,
    },
    data() {
        return {
            img:'data:image/jpeg;base64,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    ',
            resume: {
                photo: 'img/users/1.png',
                name: 'Mariana Anderson',
                position: 'Marketing Manager',
                phone: '123-456-7890',
                email: 'hello@reallygreatsite.com',
                stars:4.5,
                address: '123 Anywhere St., Any City',
                description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea distinctio est repellat eaque harum nostrum perferendis ipsa voluptate iste, necessitatibus dolore ducimus praesentium, modi consequatur, assumenda sint at laboriosam neque.',
                rating: [
                    { name: 'Regularity', stars: 5 },
                    { name: 'Accuracy', stars: 4.5 },
                    { name: 'Performance', stars: 3 },
                    { name: 'Punctuality', stars: 4.5 },
                    { name: 'Health', stars: 2 },
                    { name: 'Trustful', stars: 4 },
                    { name: 'Efficiency', stars: 3 },
                ],
                education: [
                    { year: '2008', degree: 'Enter Your Degree', school: 'University/College' },
                    { year: '2008', degree: 'Enter Your Degree', school: 'University/College' }
                ],
                expertise: ['UI/UX', 'Visual Design', 'Wireframes', 'Storyboards', 'User Flows', 'Process Flows'],
                languages: ['English', 'Spanish'],
                skills: [
                    { skill: 'HTML', percent: '100' },
                    { skill: 'CSS3', percent: '50' },
                    { skill: 'JavaScript', percent: '75' },
                    { skill: 'jQuery', percent: '50' },
                    { skill: 'Php', percent: '25' },
                    { skill: 'sql', percent: '75' },
                ],
                certificates: [
                    { year: '2015', degree: 'Certification in UI/UX', school: 'Certification Authority' },
                    { year: '2015', degree: 'Certification in Visual Design', school: 'Certification Authority' },
                    { year: '2015', degree: 'Certification in Wireframes', school: 'Certification Authority' },
                ],
                experience: [
                    {
                        period: '2019 - 2022',
                        company: 'Company Name | 123 Anywhere St., Any City',
                        position: 'Job position here',
                        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea distinctio est repellat eaque harum nostrum perferendis ipsa voluptate iste, necessitatibus dolore ducimus praesentium, modi consequatur, assumenda sint at laboriosam neque.'
                    },
                    {
                        period: '2019 - 2022',
                        company: 'Company Name | 123 Anywhere St., Any City',
                        position: 'Job position here',
                        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea distinctio est repellat eaque harum nostrum perferendis ipsa voluptate iste, necessitatibus dolore ducimus praesentium, modi consequatur, assumenda sint at laboriosam neque.'
                    },
                    {
                        period: '2019 - 2022',
                        company: 'Company Name | 123 Anywhere St., Any City',
                        position: 'Job position here',
                        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea distinctio est repellat eaque harum nostrum perferendis ipsa voluptate iste, necessitatibus dolore ducimus praesentium, modi consequatur, assumenda sint at laboriosam neque.'
                    },

                ],
                references: [
                    {
                        name: 'Name Surname',
                        position: 'Job position',
                        company: 'Company Name',
                        phone: '123-456-7890',
                        email: 'hello@reallygreatsite.com'
                    },
                    {
                        name: 'Name Surname',
                        position: 'Job position',
                        company: 'Company Name',
                        phone: '123-456-7890',
                        email: 'hello@reallygreatsite.com'
                    },

                ]
            }
        }
    }
}
</script>
<style scoped>
.order-stepper {
    display: flex;
    flex-direction: column;
}

.order-stepper #step {
    position: relative;
    padding-left: 20px;
    margin-bottom: 20px;
}

.order-stepper #step:before {
    content: '';
    position: absolute;
    top: 8px;
    left: 0;
    width: 10px;
    height: 10px;
    border-radius: 50%;
}

.order-stepper .active:before {
    background-color: green;
}

.order-stepper #step:after {
    content: '';
    position: absolute;
    top: 10px;
    left: 5px;
    height: 100%;
    border-left: 2px dashed green;
}

.order-stepper #step:last-child:after {
    content: '';
    position: absolute;
    top: 10px;
    left: 5px;
    height: calc(100% + 20px);
    /* Extend the line beyond the last step */
    border-left: 2px dashed green;
}

.timeline {
    position: relative;
    /* max-width: 1200px; */
    margin: 0 auto;
}

.timeline::after {
    content: '';
    position: absolute;
    width: 6px;
    background-color: #333;
    top: 0;
    bottom: 0;
    left: 50%;
    margin-left: -3px;
}

.timeline-item {
    padding: 10px 40px;
    position: relative;
    background-color: inherit;
    width: 50%;
}

.timeline-item::after {
    content: '';
    position: absolute;
    width: 25px;
    height: 25px;
    right: -12px;
    background-color: white;
    border: 4px solid #FF9F55;
    top: 15px;
    border-radius: 50%;
    z-index: 1;
}

.timeline-item:nth-child(odd) {
    left: 0;
}

.timeline-item:nth-child(even) {
    left: 50%;
}

.timeline-item:nth-child(even)::after {
    left: -12px;
}

 
@media screen and (max-width: 600px) {
    .timeline::after {
        left: 31px;
    }

    .timeline-item {
        width: 100%;
        padding-left:60px;
        padding-right: 25px;
    }

    .timeline-item::after {
        left: 18px !important;
    }

    .timeline-item:nth-child(even) {
        left: 0%;
    }
}
</style>