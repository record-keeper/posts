# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-20T11:40:02.088269+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×44 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×114 (24h)
- 🔴 PSI_DRIFT_DETECTED×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×38  [2026-06-20T11:02:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-06-20T11:02:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-20T11:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-06-20T10:50:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-06-20T10:47:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×59  [2026-06-20T10:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-20T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S00: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.79 ROI_boot95=[0.55,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=136 hit%=29.4% hit_CI[Bonf]=[19.6,41.6]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=136<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=35.9% hit_CI[Bonf]=[22.3,52.2]% ROI=0.58 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-20T06:00:16]
- key: `ORPHAN_SCAN|146 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.84 (コスト 10,100/回収 8,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=12.9% ROI=0.21 (コスト 6,900/回収 1,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=31.9% ROI=0.76 (コスト 16,200/回収 12,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=24.3% ROI=1.07 (コスト 8,700/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-20T06:00:16]
- key: `CALIBRATION_LIVE|bt=win: n=358 pred=0.4734 actual=0.3017 error=+0.1717 (+36%) brier=0.2404 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.51MB / last modified 2026-06-20T11:39:23.489290+09:00

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
n 1s
2026-06-20 11:38:28,753 [INFO] scraper: odds3t: 120/120 parsed
2026-06-20 11:38:29,867 [INFO] scraper: odds3f: 20/20 parsed
2026-06-20 11:38:31,001 [INFO] scraper: odds2t: 30/30 parsed
2026-06-20 11:38:31,002 [INFO] scraper: odds2f: 15/15 parsed
2026-06-20 11:38:32,127 [INFO] scraper: odds_win: 5/6 parsed
2026-06-20 11:38:32,127 [INFO] scraper: fetch_race 02/3: boats=6 odds=190/191
2026-06-20 11:38:32,138 [INFO] predictor: CALIBRATION_MODE=on
2026-06-20 11:38:32,138 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-20 11:38:33,693 [INFO] run_cycle: fetched 02/3 [scan]: 155 combos
2026-06-20 11:38:33,924 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-20 11:39:06,070 [INFO] run_cycle: === run_cycle 11:39:06 ===
2026-06-20 11:39:06,070 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-20 11:39:06,070 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-20 11:39:06,118 [INFO] predictor: Models loaded OK
2026-06-20 11:39:18,245 [INFO] scraper: odds3t: 120/120 parsed
2026-06-20 11:39:19,353 [INFO] scraper: odds3f: 19/20 parsed
2026-06-20 11:39:20,468 [INFO] scraper: odds2t: 30/30 parsed
2026-06-20 11:39:20,469 [INFO] scraper: odds2f: 11/15 parsed
2026-06-20 11:39:21,575 [INFO] scraper: odds_win: 4/6 parsed
2026-06-20 11:39:21,575 [INFO] scraper: fetch_race 11/4: boats=6 odds=184/191
2026-06-20 11:39:21,578 [INFO] predictor: CALIBRATION_MODE=on
2026-06-20 11:39:21,578 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-20 11:39:21,582 [INFO] run_cycle: fetched 11/4 [scan]: 154 combos
2026-06-20 11:39:21,620 [INFO] race_id: notif: nid=2026062011041152 sid=S00 phase=scan rank=S
2026-06-20 11:39:22,427 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 11:39:23,115 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 11:39:23,247 [INFO] run_cycle: SCAN S00 びわこ4R S
2026-06-20 11:39:23,408 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 89
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 89
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 14, 'scan': 39}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 175
  FINAL_MISSING: 114
  PSI_DRIFT_DETECTED: 44
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 15
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 9 | 8,700 | 8,280 | -420 | 0.952 |
| S01_NAKAANA1 | 30 | 8 | 6,000 | 4,900 | -1,100 | 0.817 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 1,520 | -880 | 0.633 |

## 直近アラート (24h・新しい順)
```
[11:39:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[11:38:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[11:37:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1123}
[11:36:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[11:34:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1132}
[11:33:30] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 288, "n_recent": 71, "psi": 0.296}
[11:33:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1126}
[11:32:35] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 288, "n_recent": 70, "psi": 0.573}
[11:32:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1125}
[11:31:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
```

## 本日残レース: 139件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 29件 締切済
- 通知発射: scan=8 nid / final=8 nid / result=0 nid
- predictions: 3 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 093R | win | 1 | 0.1720 | 11.2 | 1.93 | 300 | scan=12.0 drift=-6.7% | 11:33:22 |
| S01_NAKAANA1 | 022R | win | 1 | 0.3177 | 3.4 | 1.08 | 200 | scan=- drift=- | 11:13:33 |
| S01_NAKAANA1 | 172R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=- drift=- | 11:11:21 |
| S02_TETSUBAN | 2012R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 22:51:45 |
| S02_TETSUBAN | 201R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=2.0 drift=+5.0% | 17:38:39 |
| S01_NAKAANA1 | 0210R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=4.0 drift=-12.5% | 15:18:20 |
| S00 | 119R | win | 1 | 0.5476 | 6.2 | 3.40 | 300 | scan=- drift=- | 14:37:22 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5990 | 4.3 | 2.58 | 200 | scan=- drift=- | 14:23:23 |
| S00 | 178R | win | 1 | 0.5990 | 4.3 | 2.58 | 300 | scan=- drift=- | 14:23:22 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5008 | 3.0 | 1.50 | 200 | scan=4.5 drift=-33.3% | 14:09:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | -5.9% | -61.4% | +43.3% | 16 | 9 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 499.6s |
| **Latency** (scan→final max) | 618.2s |
| **Traffic** (notifications 24h) | 89 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 356 | 0.4737 | 0.2978 | +0.1759 | 🟡+37% | 0.2398 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 143 | 0.4263 | 0.2727 | 0.2189 | 🔴-0.10 | 0.78 |
| S01_NAKAANA1 | win | 135 | 0.4877 | 0.2889 | 0.2463 | 🔴-0.20 | 0.762 |
| S02_TETSUBAN | win | 78 | 0.5364 | 0.3590 | 0.2668 | 🔴-0.16 | 0.585 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 10 | 0.2246 | 0.1000 | 🔴+0.1246 |
| 0.30-0.50 | 124 | 0.4217 | 0.2661 | 🔴+0.1556 |
| 0.50+ | 207 | 0.5429 | 0.3382 | 🔴+0.2047 |

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
_auto-generated by claude_snapshot.py at 2026-06-20T11:40:02.088269+09:00_