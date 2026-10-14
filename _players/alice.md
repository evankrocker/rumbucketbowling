---
layout: player
title: Alice
player_slug: alice
permalink: /players/alice/
---

{% assign player = site.data.players | where: "slug", page.player_slug | first %}

<section class="page-header">
  <p class="eyebrow">Player profile</p>
  <h1>{{ player.name }}</h1>
</section>

<section class="panel stats-grid">
  <div class="stat-box">
    <span class="label">Season Rank</span>
    <strong>#{{ player.season_rank }}</strong>
  </div>
  <div class="stat-box">
    <span class="label">Current Week</span>
    <strong>{{ player.current_week_total }}</strong>
  </div>
  <div class="stat-box">
    <span class="label">Season Total</span>
    <strong>{{ player.season_total }}</strong>
  </div>
  <div class="stat-box">
    <span class="label">Joined</span>
    <strong>{{ player.join_date }}</strong>
  </div>
</section>

<section class="panel">
  <h2>Weekly results</h2>
  <div class="score-list">
    {% for week in site.data.weeks | sort: "week" %}
      {% assign week_score = week.scores | where: "player", player.slug | first %}
      {% if week_score %}
        <article class="score-card">
          <div class="card-header">
            <h3><a href="{{ '/weeks/' | relative_url }}{{ week.slug }}/">{{ week.title }}</a></h3>
            <span>Rank {{ week_score.rank }}</span>
          </div>
          <p class="date">{{ week.date }}</p>
          <div class="games-inline">
            <span>Game 1: {{ week_score.games[0] }}</span>
            <span>Game 2: {{ week_score.games[1] }}</span>
            <span>Game 3: {{ week_score.games[2] }}</span>
          </div>
          <p class="total-label">Weekly total: <strong>{{ week_score.total }}</strong></p>
        </article>
      {% endif %}
    {% endfor %}
  </div>
</section>
