# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-14T13:00:02.010191+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×135 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×53 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-14T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-14T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-08-14T12:46:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×114  [2026-08-14T12:03:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×114  [2026-08-14T12:03:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-08-14T12:03:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-08-14T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=46 hit%=26.1% ROI=0.53 (コスト 10,600/回収 5,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=22.2% ROI=0.90 (コスト 10,000/回収 9,000)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S00: n=172 hit%=21.5% hit_CI[Bonf]=[13.9,31.8]% ROI=0.60 ROI_boot95=[0.41,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=169 hit%=20.7% hit_CI[Bonf]=[13.2,31.0]% ROI=0.61 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-14T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-14T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=53.5% hit_CI[Bonf]=[37.0,69.3]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-14T06:00:08]
- key: `ORPHAN_SCAN|190 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.62 (コスト 11,000/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=30.6% ROI=0.77 (コスト 8,800/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-14T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=26.1% ROI=0.56 (コスト 16,100/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-14T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=412 pred=0.4671 actual=0.2670 error=+0.2001 (+43%) brier=0.2363 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.42MB / last modified 2026-08-14T13:00:04.205721+09:00

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
03,817 [INFO] predictor: Models loaded OK
2026-08-14 12:59:14,852 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=03&hd=20260814: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-14 12:59:27,271 [INFO] scraper: odds3t: 120/120 parsed
2026-08-14 12:59:28,354 [INFO] scraper: odds3f: 20/20 parsed
2026-08-14 12:59:29,478 [INFO] scraper: odds2t: 30/30 parsed
2026-08-14 12:59:29,479 [INFO] scraper: odds2f: 15/15 parsed
2026-08-14 12:59:30,576 [INFO] scraper: odds_win: 5/6 parsed
2026-08-14 12:59:30,576 [INFO] scraper: fetch_race 03/5: boats=6 odds=190/191
2026-08-14 12:59:30,579 [INFO] predictor: CALIBRATION_MODE=on
2026-08-14 12:59:30,579 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-14 12:59:30,583 [INFO] run_cycle: fetched 03/5 [final]: 155 combos
2026-08-14 12:59:34,056 [INFO] scraper: odds3t: 120/120 parsed
2026-08-14 12:59:35,128 [INFO] scraper: odds3f: 20/20 parsed
2026-08-14 12:59:36,221 [INFO] scraper: odds2t: 30/30 parsed
2026-08-14 12:59:36,222 [INFO] scraper: odds2f: 15/15 parsed
2026-08-14 12:59:37,333 [INFO] scraper: odds_win: 5/6 parsed
2026-08-14 12:59:37,333 [INFO] scraper: fetch_race 17/5: boats=6 odds=190/191
2026-08-14 12:59:37,336 [INFO] predictor: CALIBRATION_MODE=on
2026-08-14 12:59:37,336 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-14 12:59:37,340 [INFO] run_cycle: fetched 17/5 [scan]: 155 combos
2026-08-14 12:59:37,573 [INFO] race_id: notif: nid=2026081417051305 sid=S00 phase=scan rank=S
2026-08-14 12:59:37,904 [INFO] notifier: Discord notify OK (status=204)
2026-08-14 12:59:38,451 [INFO] notifier: Discord notify OK (status=204)
2026-08-14 12:59:38,646 [INFO] run_cycle: SCAN S00 宮島5R S
2026-08-14 12:59:41,055 [WARNING] scraper: beforeinfo parse failed: jcd=21 rno=10
2026-08-14 12:59:41,055 [WARNING] run_cycle: fetch None: 21/10
2026-08-14 12:59:41,162 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 98
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 98
  }
]
```

## Phase別通知記録 (24h)
{'final': 39, 'result': 22, 'scan': 37}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 135
  ANOMALY_SCRAPER_FAILURE_BURST: 110
  CIRCUIT_BREAKER_TRIP: 53
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 10 | 13,200 | 8,430 | -4,770 | 0.639 |
| S01_NAKAANA1 | 52 | 9 | 10,400 | 6,580 | -3,820 | 0.633 |
| S02_TETSUBAN | 23 | 12 | 4,600 | 3,620 | -980 | 0.787 |

## 直近アラート (24h・新しい順)
```
[12:46:47] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 11, "z_score": 2.14}
[12:33:37] CIRCUIT_BREAKER_TRIP: {"cost": 13200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 8430, "roi_7d": 0.639, "sid": "S00"}
[12:32:36] CIRCUIT_BREAKER_TRIP: {"cost": 10400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 6580, "roi_7d": 0.633, "sid": "S01_NAKAANA1"}
[12:32:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 10, "z_score": 2.14}
[12:30:57] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 8430, "roi_7d": 0.624, "sid": "S00"}
[12:15:27] FINAL_MISSING: {"deadline": "2026-08-14T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081402031145", "sid": "S00"}
[12:11:22] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 7440, "roi_7d": 0.551, "sid": "S00"}
[12:11:22] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.234, "baseline_mean": 0.766, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 8, "z_score": 2.14}
[12:03:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:32] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 61件 締切済
- 通知発射: scan=12 nid / final=12 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 034R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=3.1 drift=+54.8% | 12:32:26 |
| S00 | 024R | win | 1 | 0.3177 | 7.8 | 2.48 | 300 | scan=8.5 drift=-8.2% | 12:11:18 |
| S00 | 173R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=4.2 drift=+78.6% | 11:58:19 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=3.7 drift=+29.7% | 11:42:31 |
| S00 | 217R | win | 1 | 0.2294 | 6.1 | 1.40 | 300 | scan=- drift=- | 11:29:19 |
| S01_NAKAANA1 | 107R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=3.7 drift=-10.8% | 11:17:19 |
| S00 | 194R | win | 1 | 0.5334 | 5.5 | 2.93 | 300 | scan=4.2 drift=+31.0% | 19:00:22 |
| S00 | 019R | win | 1 | 0.1543 | 19.0 | 2.93 | 300 | scan=- drift=- | 18:49:30 |
| S02_TETSUBAN | 075R | win | 1 | 0.4111 | 2.2 | 0.90 | 200 | scan=- drift=- | 17:08:18 |
| S00 | 125R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 17:03:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 72 | +7.3% | -62.9% | +287.7% | 21 | 8 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 518.2s |
| **Latency** (scan→final max) | 615.5s |
| **Traffic** (notifications 24h) | 98 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 407 | 0.4660 | 0.2678 | +0.1982 | 🟡+42% | 0.2360 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4182 | 0.2176 | 0.2227 | 🔴-0.31 | 0.613 |
| S01_NAKAANA1 | win | 166 | 0.4886 | 0.2048 | 0.2478 | 🔴-0.52 | 0.651 |
| S02_TETSUBAN | win | 71 | 0.5276 | 0.5352 | 0.2401 | ✅+0.03 | 0.897 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 11 | 0.1834 | 0.0909 | 🔴+0.0924 |
| 0.20-0.30 | 9 | 0.2228 | 0.4444 | 🔴-0.2216 |
| 0.30-0.50 | 157 | 0.4175 | 0.2166 | 🔴+0.2010 |
| 0.50+ | 219 | 0.5427 | 0.3151 | 🔴+0.2276 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 108 | 0.771 |
| win | <5.0 | ✅learned | 183 | 0.733 |
| win | <10.0 | ✅learned | 94 | 0.45 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-14T13:00:02.010191+09:00_