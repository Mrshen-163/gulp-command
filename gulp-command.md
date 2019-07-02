var gulp = require("gulp");

var imagemin=require("gulp-imagemin");

var uglify=require("gulp-uglify");

var scss=require("gulp-sass");

var concat=require("gulp-concat");

//拷贝文件

gulp.task("copyFile", async () => {
    gulp.src("src/*.html").pipe(gulp.dest("dist"));
});

//图片压缩

gulp.task("imageMin",async()=>{
    gulp.src("src/img/*").pipe(imagemin()).pipe(gulp.dest("dist/img"))
})

//Scss转化为Css

gulp.task("mscss",async()=>{
    gulp.src("src/sass/*.scss").pipe(scss()).pipe(gulp.dest("dist/css"))
})

//合并JS

gulp.task("script",async ()=>{
    gulp.src("src/*.js").pipe(concat("main.js")).pipe(gulp.dest("dist/js"));
})

//监听SCSS文件变化

gulp.task("watch",async ()=>{
    gulp.watch("src/sass/*.scss",gulp.parallel("mscss"));
})

//执行多任务

gulp.task("default",gulp.parallel('imageMin', 'mscss', 'copyFile', async()=> {
    // Build the website.
}));
