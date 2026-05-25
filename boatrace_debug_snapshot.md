# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-25T10:50:01.852881+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×59 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-05-25T10:49:03]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-05-25T10:38:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-05-25T10:01:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×48  [2026-05-25T10:01:21]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=44 hit%=45.5% hit_CI[Bonf]=[26.3,66.1]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=44<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=44 pred=0.5098 hit=0.4545 cal_err=+0.0553 brier=0.2540 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-25T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S00: n=190 hit%=27.9% hit_CI[Bonf]=[19.6,38.1]% ROI=0.94 ROI_boot95=[0.69,1.21]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-25T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=77 hit%=28.6% hit_CI[Bonf]=[16.4,44.9]% ROI=0.75 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-25T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-25T06:00:12]
- key: `ORPHAN_SCAN|235 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.88 (コスト 14,500/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=26.8% ROI=1.14 (コスト 9,600/回収 10,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=28.1% ROI=0.86 (コスト 15,500/回収 13,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=28.0% ROI=1.11 (コスト 6,100/回収 6,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-25T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=18.9% ROI=0.53 (コスト 9,600/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.41MB / last modified 2026-05-25T10:49:03.615622+09:00

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
 scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=10&hd=20260525: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-05-25 10:48:41,083 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=10&hd=20260525: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-05-25 10:48:41,083 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=10&hd=20260525
2026-05-25 10:48:41,083 [ERROR] scraper: racelist fetch failed: jcd=10 rno=6
2026-05-25 10:48:41,083 [WARNING] run_cycle: fetch None: 10/6
2026-05-25 10:48:52,482 [INFO] scraper: odds3t: 120/120 parsed
2026-05-25 10:48:53,610 [INFO] scraper: odds3f: 19/20 parsed
2026-05-25 10:48:54,983 [INFO] scraper: odds2t: 30/30 parsed
2026-05-25 10:48:54,984 [INFO] scraper: odds2f: 12/15 parsed
2026-05-25 10:48:56,101 [INFO] scraper: odds_win: 3/6 parsed
2026-05-25 10:48:56,101 [INFO] scraper: fetch_race 17/1: boats=6 odds=184/191
2026-05-25 10:48:56,112 [INFO] predictor: CALIBRATION_MODE=on
2026-05-25 10:48:56,113 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-25 10:48:56,120 [INFO] run_cycle: fetched 17/1 [scan]: 153 combos
2026-05-25 10:48:59,651 [INFO] scraper: odds3t: 120/120 parsed
2026-05-25 10:49:00,763 [INFO] scraper: odds3f: 20/20 parsed
2026-05-25 10:49:01,935 [INFO] scraper: odds2t: 29/30 parsed
2026-05-25 10:49:01,937 [INFO] scraper: odds2f: 14/15 parsed
2026-05-25 10:49:03,099 [INFO] scraper: odds_win: 3/6 parsed
2026-05-25 10:49:03,099 [INFO] scraper: fetch_race 09/2: boats=6 odds=186/191
2026-05-25 10:49:03,113 [INFO] predictor: CALIBRATION_MODE=on
2026-05-25 10:49:03,113 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-05-25 10:49:03,125 [INFO] run_cycle: fetched 09/2 [scan]: 152 combos
2026-05-25 10:49:03,571 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 59
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 59
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 13, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 253
  FINAL_MISSING: 59
  KS_ODDS_DRIFT: 43
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_SPIKE: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 11 | 9,600 | 13,320 | +3,720 | 1.387 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 5,080 | -1,720 | 0.747 |
| S02_TETSUBAN | 14 | 6 | 2,800 | 1,800 | -1,000 | 0.643 |

## 直近アラート (24h・新しい順)
```
[10:49:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 795}
[10:47:25] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.553, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 6, "z_score": -8.02}
[10:45:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.487, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -7.06}
[10:43:20] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002201, "ks_stat": 0.235}
[10:43:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.387, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -5.61}
[10:39:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.637, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 4, "z_score": -9.23}
[10:38:33] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.553, "baseline_mean": 0.887, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -8.02}
[10:20:42] FINAL_MISSING: {"deadline": "2026-05-25T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052523040950", "sid": "S00"}
[10:16:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002935, "ks_stat": 0.231}
[10:04:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002615, "ks_stat": 0.233}
```

## 本日残レース: 125件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 19件 締切済
- 通知発射: scan=6 nid / final=2 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 236R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=- drift=- | 10:43:20 |
| S00 | 102R | win | 1 | 0.0918 | 5.6 | 0.51 | 300 | scan=5.4 drift=+3.7% | 09:02:23 |
| S00 | 246R | win | 1 | 0.0295 | 10.3 | 0.30 | 300 | scan=4.0 drift=+157.5% | 17:47:21 |
| S01_NAKAANA1 | 244R | win | 1 | 0.5476 | 3.9 | 2.14 | 200 | scan=3.5 drift=+11.4% | 16:57:21 |
| S00 | 243R | win | 1 | 0.5123 | 6.9 | 3.53 | 300 | scan=6.8 drift=+1.5% | 16:27:22 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.6 drift=-13.9% | 16:24:22 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 12:52:21 |
| S01_NAKAANA1 | 115R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=3.1 drift=+54.8% | 12:26:20 |
| S00 | 218R | win | 1 | 0.0402 | 5.0 | 0.20 | 300 | scan=- drift=- | 12:02:31 |
| S00 | 238R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=28.1 drift=-78.6% | 11:43:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +2.2% | -78.6% | +157.5% | 19 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 488.7s |
| **Latency** (scan→final max) | 600.1s |
| **Traffic** (notifications 24h) | 59 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 311 | 0.4547 | 0.3055 | +0.1493 | 🟡+33% | 0.2317 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 190 | 0.4302 | 0.2789 | 0.2221 | 🔴-0.10 | 0.937 |
| S01_NAKAANA1 | win | 77 | 0.4837 | 0.2857 | 0.2429 | 🔴-0.19 | 0.747 |
| S02_TETSUBAN | win | 44 | 0.5098 | 0.4545 | 0.2540 | 🔴-0.02 | 0.827 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 15 | 0.0082 | 0.0667 | 🔴-0.0585 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 139 | 0.4201 | 0.2590 | 🔴+0.1611 |
| 0.50+ | 145 | 0.5405 | 0.3724 | 🔴+0.1681 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 20 | 0.744 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-25T10:50:01.852881+09:00_