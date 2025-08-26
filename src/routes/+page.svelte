<script>
  let name = "홍길동";
  let title = "웹 개발자";
  let skills = ["HTML/CSS", "JavaScript", "SvelteKit", "Node.js"];
</script>

<section class="hero">
  <h1>안녕하세요, {name}입니다</h1>
  <p class="subtitle">{title}</p>
  
  <div class="intro">
    <p>
      웹 개발에 열정을 가진 개발자입니다. 
      사용자 경험을 중시하며 깔끔하고 효율적인 코드를 작성하려 노력합니다.
    </p>
  </div>

  <div class="skills">
    <h2>기술 스택</h2>
    <div class="skill-list">
      {#each skills as skill}
        <span class="skill-tag">{skill}</span>
      {/each}
    </div>
  </div>
</section>

<style>
  .hero {
    text-align: center;
    padding: 4rem 0;
  }

  h1 {
    font-size: 3rem;
    color: #2c3e50;
    margin-bottom: 1rem;
  }

  .subtitle {
    font-size: 1.5rem;
    color: #7f8c8d;
    margin-bottom: 2rem;
  }

  .intro {
    max-width: 600px;
    margin: 0 auto 3rem;
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .skills {
    margin-top: 3rem;
  }

  .skill-list {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;
    flex-wrap: wrap;
  }

  .skill-tag {
    background: #3498db;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
  }
</style>