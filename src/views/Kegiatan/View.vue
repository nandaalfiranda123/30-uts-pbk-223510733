<script>
export default {
    name: 'Kegiatan',
    data() {
        return {
            activities: [],
            newActivity: {
                name: '',
                date: '',
                status: 'Planned',
                completed: false
            },
            isEditing: false,
            editIndex: null,
            filter: ''
        };
    },
    computed: {
        filteredActivities() {
            if (this.filter === '') {
                return this.activities; // Jika filter kosong, kembalikan semua aktivitas
            } else if (this.filter === 'Selesai') {
                return this.activities.filter(activity => activity.completed);
            } else if (this.filter === 'Belum') {
                return this.activities.filter(activity => !activity.completed);
            } else {
                return []; // Kembalikan array kosong jika filter tidak sesuai
            }
        }
    },
    mounted() {
        this.getActivities();
    },
    methods: {
        getActivities() {
            // Panggil API atau lakukan pengisian dari sumber lainnya
            // Misalnya, saya menggantinya dengan data palsu untuk simulasi
            this.activities = [
                { name: 'Meeting', date: '2024-04-26', status: 'Belum Selesai', completed: false },
                { name: 'Presentation', date: '2024-04-27', status: 'Belum Selesai', completed: false },
                { name: 'Zoom', date: '2024-04-28', status: 'Selesai', completed: true }
            ];
        },
        addOrUpdateActivity() {
            if (this.isEditing) {
                this.activities[this.editIndex] = { ...this.newActivity, status: this.newActivity.completed ? 'Selesai' : 'Belum Selesai' };
                this.isEditing = false;
                this.editIndex = null;
            } else {
                if (this.newActivity.name.trim() !== '' && this.newActivity.date.trim() !== '') {
                    this.activities.push({ ...this.newActivity, status: this.newActivity.completed ? 'Selesai' : 'Belum Selesai' });
                }
            }
            this.clearForm();
        },
        editActivity(activity) {
            this.newActivity = { ...activity, completed: activity.status === 'Selesai' };
            this.isEditing = true;
            this.editIndex = this.activities.indexOf(activity);
        },
        removeActivity(index) {
            this.activities.splice(index, 1);
        },
        clearForm() {
            this.newActivity = {
                name: '',
                date: '',
                status: 'Planned',
                completed: false
            };
        }
    }
};
</script>
