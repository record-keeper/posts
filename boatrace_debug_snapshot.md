# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-19T15:00:02.173228+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×43 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×87 (24h)
- 🔴 PSI_DRIFT_DETECTED×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×55  [2026-06-19T14:05:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×55  [2026-06-19T14:05:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-06-19T14:00:26]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-06-19T13:35:21]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-06-19T13:14:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×58  [2026-06-19T10:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-19T06:00:19]
- key: `ORPHAN_SCAN|139 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S00: n=146 hit%=28.8% hit_CI[Bonf]=[19.3,40.5]% ROI=0.82 ROI_boot95=[0.58,1.09]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=146<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=132 hit%=29.5% hit_CI[Bonf]=[19.6,41.9]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=132<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=35.9% hit_CI[Bonf]=[22.3,52.2]% ROI=0.58 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.87 (コスト 10,200/回収 8,910)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=12.9% ROI=0.24 (コスト 6,900/回収 1,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=30.4% ROI=0.72 (コスト 16,300/回収 11,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=38 hit%=23.7% ROI=1.05 (コスト 8,900/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=22.2% ROI=0.46 (コスト 7,500/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.44MB / last modified 2026-06-19T15:00:06.214227+09:00

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
0 parsed
2026-06-19 14:58:27,206 [INFO] scraper: odds2f: 13/15 parsed
2026-06-19 14:58:28,386 [INFO] scraper: odds_win: 4/6 parsed
2026-06-19 14:58:28,386 [INFO] scraper: fetch_race 13/10: boats=6 odds=187/191
2026-06-19 14:58:28,395 [INFO] predictor: CALIBRATION_MODE=on
2026-06-19 14:58:28,395 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-19 14:58:28,403 [INFO] run_cycle: fetched 13/10 [scan]: 154 combos
2026-06-19 14:58:28,604 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-19 14:59:04,337 [INFO] run_cycle: === run_cycle 14:59:04 ===
2026-06-19 14:59:04,337 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-19 14:59:04,337 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-19 14:59:04,382 [INFO] predictor: Models loaded OK
2026-06-19 14:59:15,591 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=11&hd=20260619: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-19 14:59:28,022 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=11&hd=20260619: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-19 14:59:45,668 [INFO] scraper: odds3t: 120/120 parsed
2026-06-19 14:59:46,947 [INFO] scraper: odds3f: 20/20 parsed
2026-06-19 14:59:48,055 [INFO] scraper: odds2t: 30/30 parsed
2026-06-19 14:59:48,056 [INFO] scraper: odds2f: 15/15 parsed
2026-06-19 14:59:49,190 [INFO] scraper: odds_win: 4/6 parsed
2026-06-19 14:59:49,190 [INFO] scraper: fetch_race 11/10: boats=6 odds=189/191
2026-06-19 14:59:49,202 [INFO] predictor: CALIBRATION_MODE=on
2026-06-19 14:59:49,202 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-19 14:59:49,209 [INFO] run_cycle: fetched 11/10 [scan]: 154 combos
2026-06-19 14:59:49,341 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 79
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 79
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 14, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 206
  FINAL_MISSING: 87
  PSI_DRIFT_DETECTED: 43
  ANOMALY_SCAN_FINAL_RATIO: 37
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 10 | 8,700 | 8,610 | -90 | 0.99 |
| S01_NAKAANA1 | 28 | 9 | 5,600 | 5,960 | +360 | 1.064 |
| S02_TETSUBAN | 12 | 6 | 2,400 | 1,900 | -500 | 0.792 |

## 直近アラート (24h・新しい順)
```
[14:56:06] FINAL_MISSING: {"deadline": "2026-06-19T13:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061904041325", "sid": "S00"}
[14:52:22] FINAL_MISSING: {"deadline": "2026-06-19T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061921051018", "sid": "S00"}
[14:39:17] FINAL_MISSING: {"deadline": "2026-06-19T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061911061308", "sid": "S00"}
[14:37:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 290, "n_recent": 69, "psi": 0.572}
[14:34:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1053}
[14:33:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1050}
[14:32:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1045}
[14:31:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[14:30:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1048}
[14:29:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1049}
```

## 本日残レース: 61件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 83件 締切済
- 通知発射: scan=20 nid / final=19 nid / result=10 nid
- predictions: 12 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 119R | win | 1 | 0.5476 | 6.2 | 3.40 | 300 | scan=- drift=- | 14:37:22 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5990 | 4.3 | 2.58 | 200 | scan=- drift=- | 14:23:23 |
| S00 | 178R | win | 1 | 0.5990 | 4.3 | 2.58 | 300 | scan=- drift=- | 14:23:22 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5008 | 3.0 | 1.50 | 200 | scan=4.5 drift=-33.3% | 14:09:23 |
| S01_NAKAANA1 | 177R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 13:51:22 |
| S00 | 137R | win | 1 | 0.2290 | 8.2 | 1.88 | 300 | scan=- drift=- | 13:28:46 |
| S01_NAKAANA1 | 044R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 13:22:23 |
| S01_NAKAANA1 | 025R | win | 1 | 0.4989 | 4.0 | 2.00 | 200 | scan=3.7 drift=+8.1% | 12:41:23 |
| S01_NAKAANA1 | 219R | win | 1 | 0.5735 | 3.3 | 1.89 | 200 | scan=4.2 drift=-21.4% | 12:18:35 |
| S00 | 094R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=9.0 drift=-42.2% | 12:05:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | -6.2% | -61.4% | +43.3% | 15 | 9 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 507.7s |
| **Latency** (scan→final max) | 623.2s |
| **Traffic** (notifications 24h) | 79 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 358 | 0.4725 | 0.3045 | +0.1680 | 🟡+36% | 0.2405 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4253 | 0.2847 | 0.2202 | 🔴-0.08 | 0.81 |
| S01_NAKAANA1 | win | 137 | 0.4869 | 0.2920 | 0.2483 | 🔴-0.20 | 0.76 |
| S02_TETSUBAN | win | 77 | 0.5350 | 0.3636 | 0.2649 | 🔴-0.14 | 0.592 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 10 | 0.2246 | 0.1000 | 🔴+0.1246 |
| 0.30-0.50 | 125 | 0.4194 | 0.2800 | 🔴+0.1394 |
| 0.50+ | 208 | 0.5420 | 0.3413 | 🔴+0.2007 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 44 | 0.711 |
| win | <5.0 | ✅learned | 83 | 0.749 |
| win | <10.0 | ✅learned | 55 | 0.495 |
| win | <20.0 | ✅learned | 14 | 0.21 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-19T15:00:02.173228+09:00_