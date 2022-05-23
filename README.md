# handler
After save
const logger = Moralis.Cloud.getLogger();

Moralis.Cloud.afterSave("Comment", (request) => {
  const query = new Moralis.Query("Post");
  query
    .get(request.object.get("post").id)
    .then(function (post) {
      post.increment("comments");
      return post.save();
    })
    .catch(function (error) {
      logger.error("Got an error " + error.code + " : " + error.message);
    });
});
