const posts = [];
let lastActivityTime = 0;

function createPost(post) {
    return new Promise((resolve) => {
        setTimeout(() => {
            posts.push(post);
            resolve();
        }, 1000);
    });
}

function updateLastUserActivityTime() {
    return new Promise((resolve) => {
        setTimeout(() => {
            lastActivityTime = new Date().toLocaleTimeString();
            resolve(lastActivityTime);
        }, 1000);
    });
}

function deletePost() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (posts.length > 0) {
                const deletedPost = posts.pop();
                resolve(deletedPost);
            } else {
                reject("ERROR: No posts to delete");
            }
        }, 1000);
    });
}

createPost({ title: "Post One", body: "This is Post One" })
    .then(() => updateLastUserActivityTime())
    .then(() => {
        // After creating a post and updating the last activity time
        // Log all posts and the last activity time
        console.log("All Posts:", posts);
        console.log("Last Activity Time:", lastActivityTime);
    })
    .then(() => deletePost())
    .then(() => {
        // After deleting a post, log the remaining posts
        console.log("Remaining Posts:", posts);
    })
    .catch((error) => {
        console.error(error);
    });
