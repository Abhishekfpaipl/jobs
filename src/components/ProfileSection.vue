<template>
    <div class="container mt-5">
        <div class="row">
            <!-- Left column -->
            <div class="col-md-3 bg-dark text-white p-4 text-start">
                <div class="mb-4">
                    <img :src="resume.photo" alt="Profile Photo" class="rounded-circle img-fluid mb-3"
                        style="max-width: 150px;">
                </div>
                <h5 class="mt-4 border-bottom">Ratings</h5>
                <div class="d-flex justify-content-between align-items-center" v-for="(rating,index) in resume.rating" :key="index">
                    <p class="mb-0">{{rating.name}}</p>
                    <ReviewRating :rating="rating.stars"/>
                </div>
                
                <h5 class="mt-4 border-bottom">Contact</h5>
                <p><i class="bi bi-telephone"></i>&nbsp;: <span>{{ resume.phone }}</span></p>
                <p><i class="bi bi-envelope"></i>&nbsp;: <span>{{ resume.email }}</span></p>
                <p><i class="bi bi-geo-alt"></i>&nbsp;: <span>{{ resume.address }}</span></p>

                <h5 class="mt-4 border-bottom">Technical Skills</h5>
                <div class="" v-for="(skill, index) in resume.skills" :key="index">
                    <p class="mb-1 mt-3 text-uppercase">{{ skill.skill }} </p>
                    <div class="progress rounded-0" role="progressbar" aria-label="Danger example" aria-valuenow="100"
                        aria-valuemin="0" aria-valuemax="100">
                        <div class="progress-bar bg-danger" :style="{ width: skill.percent + '%' }"> {{ skill.percent }}
                            %</div>
                    </div>
                </div>
                <h5 class="mt-4 border-bottom">Expertise</h5>
                <ul>
                    <li v-for="skill in resume.expertise" :key="skill">{{ skill }}</li>
                </ul>

                <h5 class="mt-4 border-bottom">Language</h5>
                <ul>
                    <li v-for="lang in resume.languages" :key="lang">{{ lang }}</li>
                </ul>
            </div>

            <!-- Right column -->
            <div class="col-md-9 p-4 text-start">
                <div class="mb-4">
                    <h1>{{ resume.name }}</h1>
                    <h5>{{ resume.position }}</h5>
                    <p>{{ resume.description }}</p>
                </div>
                <h3 class="mt-4 border-bottom">Experience</h3>
                <div class="order-stepper">
                    <div v-for="(job, index) in resume.experience" :key="index" class="mb-4 active" id="step">
                        <h5>{{ job.period }}</h5>
                        <p><strong>{{ job.company }}</strong></p>
                        <p>{{ job.position }}</p>
                        <p>{{ job.description }}</p>
                    </div>
                </div>
                <h3 class="mt-4 border-bottom">Education</h3>
                <div class="row m-2" v-for="(edu, index) in resume.education" :key="index">
                    <div class="text-center col-12 fw-bold">{{ edu.year }}</div>
                    <div class="border col-6 bg-light py-3">{{ edu.degree }}</div>
                    <div class="border col-6 py-3">{{ edu.school }}</div>
                </div>
                <h3 class="mt-4 border-bottom">Certificates</h3>
                <div class="row m-2" v-for="(edu, index) in resume.certificates" :key="index">
                    <div class="text-center col-12 fw-bold">{{ edu.year }}</div>
                    <div class="border col-6 bg-light py-3">{{ edu.degree }}</div>
                    <div class="border col-6 py-3">{{ edu.school }}</div>
                </div>
                <!-- <div v-for="edu in resume.education" :key="edu.year" class="">
                    <p class="mb-1 mt-3"><strong>{{ edu.year }}</strong></p>
                    <p class="mb-1">{{ edu.degree }}</p>
                    <p class="mb-1">{{ edu.school }}</p>
                </div> -->
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
</template>

<script>
import ContactSection from "@/components/ContactSection.vue";
import ReviewRating from "@/components/ReviewRating.vue";
export default {
    name: 'ResumeComponent',
    components: {
        ContactSection,
        ReviewRating,
    },
    data() {
        return {
            resume: {
                photo: 'img/users/1.png',
                name: 'Mariana Anderson',
                position: 'Marketing Manager',
                phone: '123-456-7890',
                email: 'hello@reallygreatsite.com',
                address: '123 Anywhere St., Any City',
                description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea distinctio est repellat eaque harum nostrum perferendis ipsa voluptate iste, necessitatibus dolore ducimus praesentium, modi consequatur, assumenda sint at laboriosam neque.',
                rating:[
                    {name:'Regularity', stars:5},
                    {name:'Accuracy', stars:4.5},
                    {name:'Performance', stars:3},
                    {name:'Punctuality', stars:4.5},
                    {name:'Health', stars:2},
                    {name:'Trustful', stars:4},
                    {name:'Efficiency', stars:3},
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
</style>