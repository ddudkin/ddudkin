php artisan vendor:publish --provider "L5Swagger\L5SwaggerServiceProvider"
/**
 * @SWG\Swagger(
 *   schemes={"http"},
 *   host="localhost:8000",
 *   basePath="/",
 *   @SWG\Info(
 *     title="Blog posts API",
 *     version="1.0.0"
 *   )
 * )
 */
class Controller extends BaseController {}
php artisan make:model Post
/**
 * @SWG\Definition(
 *  definition="Post",
 *  @SWG\Property(
 *      property="id",
 *      type="integer"
 *  ),
 *  @SWG\Property(
 *      property="title",
 *      type="string"
 *  ),
 *  @SWG\Property(
 *      property="text",
 *      type="string"
 *  )
 * )
 */
class Post extends Model {}
php artisan make:controller PostsController --api
class PostsController extends Controller
{
    /**
     * @SWG\Get(
     *     path="/posts",
     *     summary="Get list of blog posts",
     *     tags={"Posts"},
     *     @SWG\Response(
     *         response=200,
     *         description="successful operation",
     *         @SWG\Schema(
     *             type="array",
     *             @SWG\Items(ref="#/definitions/Post")
     *         ),
     *     ),
     *     @SWG\Response(
     *         response="401",
     *         description="Unauthorized user",
     *     ),
     * )
     */
    public function index() {}
    /**
     * @SWG\Get(
     *     path="/posts/{post_id}",
     *     summary="Get blog post by id",
     *     tags={"Posts"},
     *     description="Get blog post by id",
     *     @SWG\Parameter(
     *         name="post_id",
     *         in="path",
     *         description="Post id",
     *         required=true,
     *         type="integer",
     *     ),
     *     @SWG\Response(
     *         response=200,
     *         description="successful operation",
     *         @SWG\Schema(ref="#/definitions/Post"),
     *     ),
     *     @SWG\Response(
     *         response="401",
     *         description="Unauthorized user",
     *     ),
     *     @SWG\Response(
     *         response="404",
     *         description="Post is not found",
     *     )
     * )
     */
    public function show($id) {}
}
php artisan l5-swagger:generate
