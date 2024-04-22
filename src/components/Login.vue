<script>
import axios from 'axios'
export default {
    name: 'AppLogin', // Changed component name to be multi-word
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            try {
                let result = await axios.post("http://localhost:3000/users", {
                    email: this.email,
                    password: this.password
                });

                if (result.status === 200 && result.data.length > 0) {
                    localStorage.setItem("user-info", JSON.stringify(result.data[0]))
                    this.$router.push({
                        name: 'Home'
                    });
                }
            } catch (error) {
                console.error("Login error:", error);
                // Handle login error (e.g., show an error message)
            }
        }
    },
    mounted() {
        let user = localStorage.getItem("user-info");
        if (user) {
            this.$router.push({
                name: 'Home'
            });
        }
    }
}
</script>
