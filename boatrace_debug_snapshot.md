# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-12T14:00:02.118630+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×107 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-07-12T13:38:33]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×29  [2026-07-12T13:29:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×108  [2026-07-12T13:03:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×54  [2026-07-12T13:03:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-12T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-12T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×14  [2026-07-12T12:46:27]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×1  [2026-07-12T11:27:20]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-07-12T09:00:06]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S00: n=168 hit%=30.4% hit_CI[Bonf]=[21.2,41.3]% ROI=0.79 ROI_boot95=[0.59,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.7% hit_CI[Bonf]=[21.2,42.2]% ROI=0.87 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=46.4% hit_CI[Bonf]=[30.4,63.1]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-12T06:00:05]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=33.3% ROI=0.87 (コスト 9,600/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.74 (コスト 10,400/回収 7,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=34.5% ROI=0.88 (コスト 20,000/回収 17,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=32 hit%=37.5% ROI=1.05 (コスト 8,000/回収 8,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.55MB / last modified 2026-07-12T14:00:02.807415+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
d=20260712: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-12 13:59:26,868 [INFO] scraper: odds3t: 120/120 parsed
2026-07-12 13:59:27,951 [INFO] scraper: odds3f: 20/20 parsed
2026-07-12 13:59:29,043 [INFO] scraper: odds2t: 30/30 parsed
2026-07-12 13:59:29,044 [INFO] scraper: odds2f: 15/15 parsed
2026-07-12 13:59:30,160 [INFO] scraper: odds_win: 6/6 parsed
2026-07-12 13:59:30,161 [INFO] scraper: fetch_race 08/8: boats=6 odds=191/191
2026-07-12 13:59:30,164 [INFO] predictor: CALIBRATION_MODE=on
2026-07-12 13:59:30,164 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-12 13:59:30,169 [INFO] run_cycle: fetched 08/8 [final]: 156 combos
2026-07-12 13:59:34,175 [INFO] scraper: odds3t: 120/120 parsed
2026-07-12 13:59:35,867 [INFO] scraper: odds3f: 20/20 parsed
2026-07-12 13:59:37,290 [INFO] scraper: odds2t: 30/30 parsed
2026-07-12 13:59:37,291 [INFO] scraper: odds2f: 14/15 parsed
2026-07-12 13:59:38,760 [INFO] scraper: odds_win: 5/6 parsed
2026-07-12 13:59:38,760 [INFO] scraper: fetch_race 23/12: boats=6 odds=189/191
2026-07-12 13:59:38,762 [INFO] predictor: CALIBRATION_MODE=on
2026-07-12 13:59:38,762 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-12 13:59:38,766 [INFO] run_cycle: fetched 23/12 [scan]: 155 combos
2026-07-12 13:59:43,317 [INFO] scraper: odds3t: 120/120 parsed
2026-07-12 13:59:44,853 [INFO] scraper: odds3f: 19/20 parsed
2026-07-12 13:59:46,234 [INFO] scraper: odds2t: 26/30 parsed
2026-07-12 13:59:46,235 [INFO] scraper: odds2f: 14/15 parsed
2026-07-12 13:59:47,328 [INFO] scraper: odds_win: 3/6 parsed
2026-07-12 13:59:47,329 [INFO] scraper: fetch_race 09/8: boats=6 odds=182/191
2026-07-12 13:59:47,331 [INFO] predictor: CALIBRATION_MODE=on
2026-07-12 13:59:47,331 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-07-12 13:59:47,335 [INFO] run_cycle: fetched 09/8 [scan]: 149 combos
2026-07-12 13:59:47,431 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 95
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 95
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 24, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 202
  FINAL_MISSING: 107
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 29
  ANOMALY_SCAN_FINAL_RATIO: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 16 | 13,500 | 11,880 | -1,620 | 0.88 |
| S01_NAKAANA1 | 42 | 10 | 8,400 | 5,120 | -3,280 | 0.61 |
| S02_TETSUBAN | 21 | 11 | 4,200 | 4,860 | +660 | 1.157 |

## 直近アラート (24h・新しい順)
```
[13:53:00] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 5120, "roi_7d": 0.61, "sid": "S01_NAKAANA1"}
[13:47:43] CIRCUIT_BREAKER_TRIP: {"cost": 8600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 5960, "roi_7d": 0.693, "sid": "S01_NAKAANA1"}
[13:38:33] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 5960, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[13:38:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1472}
[13:37:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1465}
[13:36:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1456}
[13:35:27] FINAL_MISSING: {"deadline": "2026-07-12T12:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071209041205", "sid": "S00"}
[13:34:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1449}
[13:32:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1468}
[13:31:32] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 5960, "roi_7d": 0.662, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 98件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 94件 締切済
- 通知発射: scan=19 nid / final=22 nid / result=11 nid
- predictions: 15 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 037R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 13:53:48 |
| S01_NAKAANA1 | 087R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.3 drift=+18.2% | 13:29:18 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5102 | 4.5 | 2.30 | 200 | scan=3.7 drift=+21.6% | 13:26:31 |
| S00 | 036R | win | 1 | 0.5102 | 4.5 | 2.30 | 300 | scan=4.0 drift=+12.5% | 13:26:30 |
| S01_NAKAANA1 | 064R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=3.3 drift=+21.2% | 12:46:19 |
| S00 | 034R | win | 1 | 0.2173 | 4.0 | 0.87 | 300 | scan=- drift=- | 12:33:18 |
| S00 | 239R | win | 1 | 0.5174 | 22.7 | 11.74 | 300 | scan=12.7 drift=+78.7% | 12:16:17 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5735 | 3.6 | 2.06 | 200 | scan=3.0 drift=+20.0% | 12:11:18 |
| S00 | 084R | win | 1 | 0.5174 | 7.5 | 3.88 | 300 | scan=5.2 drift=+44.2% | 11:59:17 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=- drift=- | 11:52:26 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +17.8% | -73.3% | +533.3% | 18 | 7 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.4s |
| **Latency** (scan→final max) | 624.3s |
| **Traffic** (notifications 24h) | 95 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 392 | 0.4734 | 0.3291 | +0.1443 | 🟡+30% | 0.2362 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4369 | 0.2965 | 0.2267 | 🔴-0.09 | 0.753 |
| S01_NAKAANA1 | win | 153 | 0.4849 | 0.3072 | 0.2378 | 🔴-0.12 | 0.833 |
| S02_TETSUBAN | win | 67 | 0.5405 | 0.4627 | 0.2570 | 🔴-0.03 | 0.903 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1783 | 0.6000 | 🔴-0.4217 |
| 0.20-0.30 | 15 | 0.2280 | 0.2000 | ✅+0.0280 |
| 0.30-0.50 | 143 | 0.4192 | 0.2937 | 🔴+0.1255 |
| 0.50+ | 223 | 0.5413 | 0.3632 | 🔴+0.1781 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 69 | 0.79 |
| win | <5.0 | ✅learned | 135 | 0.711 |
| win | <10.0 | ✅learned | 71 | 0.467 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-07-12T14:00:02.118630+09:00_